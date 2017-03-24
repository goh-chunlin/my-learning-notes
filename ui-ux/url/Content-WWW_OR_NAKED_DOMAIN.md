# To WWW Or Not - That's The Problem

There is always a question from especially startups asking which one, www or **Naked Domain** (i.e. the one without www), is better for the SEO of their new website. Naked domains, also called bare or apex domains, are configured in DNS via **A Records**.

## UX
From User Experience point of view, it is not recommended to use www in URLs of our websites. There are few reasons as follows.
 - KISS Principle: Keep It Short and Simple;
 - It's extra typing for the user, or speaking - www is actually quite a mouthful when reading out a web address. "Dub dub dub" huh?
 - Naked domain makes the URL easy to remember, unless the domain name itself is long also;
 - Having www in a URL will make the URL to be longer and thus people feel difficult to share our website on Twitter which forces the input to be at most 144 characters long. Hence, it's better to keep the URL short.

Meanwhile, there are also people who disagree to use naked domain from User Experience point of view. They believe that the www clearly conveys that is the address on the World Wide Web and people are used to seeing the www.

## SEO
For average users, to use either www.example.com or just example.com for their website main domain, there isn't so much difference. In fact, it has almost no effect on SEO, according to [Google Search Console Help](https://support.google.com/webmasters/answer/44231?hl=en).

> Links may point to your site using both the www and non-www versions of the URL (for instance, http://www.example.com and http://example.com).
>
> Once you tell us your preferred domain name, we use that information for all future crawls of your site and indexing refreshes.
>
> -- Google Search Console Help

What Google Search Console suggests is that we still need to verify ownership of both the www and non-www versions of our domain. After that, in the **Preferred domain** section in [Google Search Console (fka Google Web Masters Tool)](https://www.google.com/webmasters/tools/home?hl=en), we just need to specify which domain we want to use, www or without www.

As a nontechincal SEO advantage of a naked domain is SERP (Search Engine Results Page) results - more space in the SERP result to display URL of the result page. If you have a deep URL structure with long names - this can become very handy to help increase SERP CTR (Click-Through Rate).

## Cookies
If our app sets cookies to naked domain example.com, cookies will also be available for all subdomains *.example.com. Hence, the cookies will possibly interfere with cookie used on other subdomains. For example, if our static content is served from subdomain static.example.com, we need to go with www. Doing so, we can then make the static content subdomain static.example.com cookieless, thus improving performance because using no www will set domain-level cookies and send them for all requests. Twitter, for instance, which does not use www, had to buy new domain names, such as twimg.com, just for static content.

However, this is not a bad news if we want to explicitly share the cookies across all our subdomains, for instance to implement single sign-on across various services on subdomains of our website.

In addition, people who don't think this is an issue also believe that cookies are extremely small text files. So to them, even if cookies are sent with each HTTP request, the additional transfer of a few hundred bytes would go virtually unnoticed.

## Microsoft Azure Traffic Manager
Another reason why we need www has to do with the use of DNS and the CNAME record.

Naked domains are configured in DNS via A Records and thus have serious availability implications when used in highly available environments such as cloud infrastructure services and platforms like Microsoft Azure and Heroku.

In Microsoft Azure, **Traffic Manager** geo-route incoming traffic to our app to distribute the traffic so that the availability and performance of our app is improved. If Traffic Manager have an issue with routing, or there is DDOS attack against that specific address, they are not able to update our zone's A record to point to a different IP on the fly; they can update their own, though, and that's what a CNAME allows them to do. Hence, we need to create a CNAME DNS record, for example www.example.com, that maps to the domain name of our Traffic Manager profile.

```
www.example.com IN CNAME example.trafficmanager.net
```

**ALIAS** (or ANAME records) can achieve the same results as the CNAME on naked domain. [The ALIAS record maps a name to another name, but in turns it can coexist with other records on that name.](https://support.dnsimple.com/articles/differences-between-a-cname-alias-url/) However, ANAME records are not a standard **DNS Resource Records** type. They are proprietary to specific service providers.

## Choose One and Stick with It
Once we've set our preferred domain, we need to use a **301 Redirect** to redirect traffic from non-www (or www) domain to www (or non-www), so that search engines and visitors know which version we prefer. What's important is that we must stay consistent with the one that we chose at the time of starting our website. **DO NOT CHANGE** the site URL after opening your website.

### 301 Redirect using web.config in ASP .NET
To redirect from naked domain to one with www, please have the following rewrite rule.

```
<rewrite>
  <rules>
  
    ...
  
    <rule name="Redirect example.com to www.example.com" patternSyntax="Wildcard" stopProcessing="true">
      <match url="*" />
      <conditions>
        <add input="{HTTP_HOST}" pattern="example.com" />
      </conditions>
      <action type="Redirect" url="http://www.example.com/{R:0}" />
    </rule>
  </rules>
</rewrite>
```

To redirect from domain with www to naked domain, please have the following rewrite rule.

```
<rewrite>
  <rules>
  
    ...
  
    <rule name="Redirect www.example.com to example.com" stopProcessing="true">
      <match url="(.*)" ignoreCase="true" />
      <conditions>
        <add input="{HTTP_HOST}" pattern="^www\.example\.com$" />
      </conditions>
      <action type="Redirect" url="http://www.example.com/{R:1}" redirectType="Permanent" />
    </rule>
  </rules>
</rewrite>
```

## References
 - [Set your preferred domain (www or non-www)](https://support.google.com/webmasters/answer/44231?hl=en)
 - [‘WWW’ Is Out. Naked Domains Are In!](https://uptownstudios.net/www-is-out-naked-domains-are-in/)
 - [Cons of redirecting www to no-www (naked domain name) and vice versa - Stack Overflow](http://stackoverflow.com/a/36947489/1177328)
 - [www vs non-www which is better?](https://moz.com/community/q/www-vs-non-www-which-is-better)
 - [WWW vs non-WWW – Which is Better For WordPress SEO?](http://www.wpbeginner.com/beginners-guide/www-vs-non-www-which-is-better-for-wordpress-seo/)
 - [To www or Not to www — That is the Question](https://www.sitepoint.com/domain-www-or-no-www/)
 - [Why use www?](http://www.yes-www.org/why-use-www/)
 - [What’s the point in having “www” in a URL? - Server Fault](http://serverfault.com/questions/145777/what-s-the-point-in-having-www-in-a-url)
 - [Differences between the A, CNAME, ALIAS and URL records](https://support.dnsimple.com/articles/differences-between-a-cname-alias-url/)
 - [Why does Heroku warn against “naked” domain names?](http://serverfault.com/questions/408017/why-does-heroku-warn-against-naked-domain-names)
 - [Microsot Azure Traffic Manager](https://azure.microsoft.com/en-us/services/traffic-manager/)
