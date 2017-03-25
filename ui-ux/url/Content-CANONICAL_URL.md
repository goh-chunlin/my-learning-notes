# Canonical URL

## What and Why?
Most of the time, the **same and equivalent** web content can be accessed through multiple URLs, eg. `https://example.com/attraction?productId=12` and `https://example.com/attraction/singapore-uss` are pointing to the same product page of Singapore USS attraction. However, this has created some challenges to the search engine because, for example, with a variety of URLs, it's more challenging to get consolidated metrics for a specific piece of content.

To address these issues, we are recommended to define a canonical URL for equivalent content available through multiple URLs.

## The `rel="canonical"` Link Element
Based on the example above, suppose we want the preferred URL to be `https://example.com/attraction/singapore-uss`, even though a variety of URLs can access this content. We can indicate this to search engines by marking up the canonical page and any other variants with a **`rel="canonical"` Link Element**.

To do so, we simply add a **<link> element** with the attribute rel="canonical" to the **<head> section** of these pages:

```
<link rel="canonical" href="https://example.com/attraction/singapore-uss" />
```

This indicates the preferred URL to use to access the Singapore USS attraction page, so that the SERP (Search Engine Results Page) will be more likely to show users that URL structure. (Note: Search engines like Google attempt to respect this, but cannot guarantee this in all cases.)

**NOTE:** We must use **absolute paths** rather than relative paths with the `rel="canonical"` link element.

If we can configure our server, we can use rel="canonical" HTTP headers to indicate the canonical URL for HTML documents and other files such as PDFs.

```
Link: <http://www.example.com/attraction/terms-and-conditions.pdf>; rel="canonical"
```

Google also prefers HTTPS pages over equivalent HTTP pages as canonical. We can ensure this behavior by taking any of the following actions:
 - Add 301 redirect from the HTTP page to the HTTPS page;
 - Add a `rel="canonical"` link from the HTTP page to the HTTPS page;
 - Implement **HSTS (HTTP Strict Transport Security)**.
 
### 301 Redirect or Canonical?
If there are no technical reasons not to do a redirect, we should always do a 301 redirect. If the redirect would break the user experience or be otherwise problematic, please set a canonical URL.

### Self-Referencing Canonical URL
Having a canonical link element on every web page is confirmed to be the best practice.

In most of the ASP .NET websites, we are allowed to key in random query string without changing the content. So all of these URLs would show the same content:

```
https://example.com/attraction/singapore-uss
https://example.com/attraction/singapore-uss?test=123
https://example.com/attraction/singapore-uss?oh-my-god=omg
```

Hence, if we don't have a self-referencing canonical on the page that points to the cleanest version of the URL, there will be a risk of being hit by this stuff. Hence, adding a self-referencing canonical to URLs across our site is a good defensive SEO move.
 
### HSTS and Its Implementation
> HSTS is a way to keep you from inadvertently switching AWAY from SSL once you've visited a site via HTTPS. For example, you'd hate to go to your bank via HTTPS, confirm that you're secure and go about your business only to notice that at some point you're on an insecure HTTP URL.
>
> ...
>
> HSTS is a way of saying "seriously, stay on HTTPS for this amount of time (like weeks). If anyone says otherwise, do an Internal Redirect and be secure anyway."
>
> -- Scott Hanselman, [How to enable HTTP Strict Transport Security (HSTS) in IIS7+](http://www.hanselman.com/blog/HowToEnableHTTPStrictTransportSecurityHSTSInIIS7.aspx)

To implement HSTS in ASP .NET, we need to add **Strict-Transport-Security**, the CustomHeader required for HSTS in web.config.

However, Strict-Transport-Security should not be sent over HTTP. It should be sent over HTTPS. Thus, we need to implement as such.

```
<rewrite>
  <rules>
  
    ...
  
    <rule name="HTTP to HTTPS redirect" stopProcessing="true">
      <match url="(.*)" />
      <conditions>
        <add input="{HTTPS}" pattern="off" ignoreCase="true" />
      </conditions>
      <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent" />
    </rule>
  </rules>
  <outboundRules>
    <rule name="Add Strict-Transport-Security when HTTPS" enabled="true">
      <match serverVariable="RESPONSE_Strict_Transport_Security" pattern=".*" />
      <conditions>
        <add input="{HTTPS}" pattern="on" ignoreCase="true" />
      </conditions>
      <action type="Rewrite" value="max-age=31536000" />
    </rule>
  </outboundRules>
</rewrite>
```

The first rule shown above directs user from insecured HTTP to a secure location (HTTPS). The second one adds the HTTP header for Strict-Transport-Security.

With HSTS implemented, we can solve the problem of SSLStrip. **SSLStrip** is a type of Man-In-The-Middle attack that forces a victim's browser into communicating with attacker in plain-text over HTTP, and the attacker proxies the modified content from an HTTPS server. To do this, SSLStrip is "stripping"  https:// URLs and turning them into http:// URLs.

```
Victim  <== HTTP ==>  Attacker  <== HTTPS ==>  Secured Site
```

#### Secured Cookies
In addition, we also must take care of our cookies by setting all of them by default to be **HttpOnly** and **SslOnly** in web.config.

```
<system.web>
  <httpCookies httpOnlyCookies="true" requireSSL="true"/>
</system.web>
```

## Implementation of Canonical Link in ASP .NET MVC with Aspect Oriented Programming (AOP)
Firstly, we define a **Custom Action Filter** by creating an action filter as an attribute that inherits from the ActionFilterAttribute class.

```
public class CanonicalFilterAttribute : ActionFilterAttribute
{
  public string CanonicalUrl;

  public override void OnResultExecuting(ResultExecutingContext filterContext)
  {
    string language = filterContext.RouteData.Values["language"].ToString(); // This is for localization of the website

    filterContext.Controller.ViewBag.CanonicalUrl = $"https://example.com/{language}/{CanonicalUrl}";
  }
}
```
The **OnResultExecuting** method is called just before the ActionResult instance that is returned by the action is invoked.

Secondly, we just decorate the action methods with this canonical action filter.

```
[CanonicalFilter(CanonicalUrl = "attractions")]
public ActionResult Index()
{
  ...
}
```

Finally, at the View, we need to define the following.

```
@if (ViewBag.CanonicalUrl != null) {
  <link rel="canonical" href="@ViewBag.CanonicalUrl" />
}
```

## Let Google Decides
When Google detects duplicate content, such as the pages in the example above, a Google algorithm groups the duplicate URLs into one cluster and selects what the algorithm thinks is the best URL to represent the cluster in search result. Google then tries to consolidate what we know about the URLs in the cluster, such as link popularity, to the one representative URL to ultimately improve the accuracy of its page ranking and results in Google Search.

However, when Google can't find all the URLs in a cluster or is unable to select the representative URL that we prefer, we can use the [URL Parameters tool](https://www.google.com/webmasters/tools/crawl-url-parameters) to give Google information about how to handle URLs containing specific parameters.

**NOTE:** We should be **extra careful** when using the URL Parameters tool. Any mistake in indicating to Google what is duplicate content that should not be crawled, Google might stop crawling pages we want available on Google Search.

## References
 - [Use canonical URLs](https://support.google.com/webmasters/answer/139066?visit_id=1-636260078706177599-1436413797&rd=1)
 - [Learn the impact of duplicate URLs](https://support.google.com/webmasters/answer/6080548?visit_id=1-636260078706177599-1436413797&rd=1)
 - [Using Rel Canonical on All Pages for Duplicate Content Protection](http://www.thesempost.com/using-rel-canonical-on-all-pages-for-duplicate-content-protection/)
 - [English Google Webmaster Central office-hours hangout - YouTube Video](https://www.youtube.com/watch?v=pXrwAM898oY)
 - [How to enable HTTP Strict Transport Security (HSTS) in IIS7+](http://www.hanselman.com/blog/HowToEnableHTTPStrictTransportSecurityHSTSInIIS7.aspx)
 - [Enable HTTP Strict Transport Security (HSTS) in IIS 7 - Stack Overflow](http://serverfault.com/a/629594)
 - [Implementing HTTPS Everywhere in ASP.Net MVC application.](http://tech.trailmax.info/2014/02/implemnting-https-everywhere-in-asp-net-mvc-application/)
 - [How does SSLstrip work? - Information Security Stack Exchange](https://security.stackexchange.com/questions/41988/how-does-sslstrip-work)
 - [Aspect Oriented Programming in ASP.NET MVC](http://stackoverflow.com/questions/23244400/aspect-oriented-programming-in-asp-net-mvc)
 - [How to: Create a Custom Action Filter - MSDN](https://msdn.microsoft.com/en-us/library/dd410056(v=vs.98).aspx)
 - [Creating Custom Action Filters - MSDN](https://msdn.microsoft.com/en-us/library/dd381609(v=vs.98).aspx)
