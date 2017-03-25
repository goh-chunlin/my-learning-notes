# Trailing Slash
A **Trailing Slash** is the forward slash (/) placed at the end of a URL.

## To Slash or Not - That's The Problem
Historically, it’s common for URLs with a trailing slash to indicate a directory, and those without a trailing slash to denote a file:

```
http://example.com/foo/ (with trailing slash, conventionally a directory)
```

```
http://example.com/foo (without trailing slash, conventionally a file)
```

Google treats each URL above separately and equally regardless of whether it's a file or a directory, or it contains a trailing slash or it doesn't contain a trailing slash.

## SEO: Trailing Slash is Evil
In an ideal world, there's a one-to-one pairing between URL and content: each URL leads to a unique piece of content, and each piece of content can only be accessed via one URL. The closer we can get to this ideal, the more streamlined our site will be for search engine crawling and indexing.

It is important to remove trailing slash from the URLs because if websites can be accessed through a URL with a different number of trailing slashes such as a page that can be opened with two or no trailing slashes, it will result in duplicate content which should be avoided. Any individual content should only be accessible through a single URL and having search engine indexing multiple URLs which point to the same page can also hurt the ranking of the website on SERP (Search Engine Results Page).

If both slash and non-trailing-slash versions contain the same content and each returns 200, please consider changing this behavior to have one of them redirected to its counterpart. This is to reduce duplicate content and improve crawl efficiency.

**Be consistent with the version of the URL used in the website.** If there is a Sitemap, please include the preferred version (and don't include the duplicate URL).

## Removing Trailing Slash in ASP.NET
To remove the trailing slash from the url of our website if there is one and make 301 permanent redirect to the new URL, please have the following rewrite rule.

```
<rewrite>
  <rules>
  
    ...
  
    <rule name="Removing trailing slash" stopProcessing="true">
      <match url="(.*)/$" />
      <conditions>
        <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
        <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
      </conditions>
      <action type="Redirect" redirectType="Permanent" url="{R:1}" />
    </rule>
  </rules>
</rewrite>
```

**Note:** In the development environment, we need to run the web site under at least IIS Express to see this feature working.

**Note:** Rest assured that for the root URL specifically, http://example.com is equivalent to http://example.com/ in Google search engine and cannot be redirected.

## Test
We can test the 301 configuration through Fetch as Google in Google Search Console by following the steps below.

 1. Login to [Google Search Console](https://www.google.com/webmasters/tools/home?hl=en);
 2. Select the website to test;
 3. Under **Dashboard** menu, expand **Crawl** and then choose **Fetch as Google**;
 3. Enter the version of the URL without trailing slash and press the **Fetch** button;
 4. Once the result is out, click on the value of the result at the **Status** column. The value should say **Completed**;
 5. HTTP Response of the URL will be generated. It should be **HTTP/1.1 200 OK**;
 6. Back to Fetch as Google, and enter the URL with the trailing slash and click on the **Fetch** button;
 7. The **Status** of the result should be **Redirected**;
 7. The HTTP Response of the URL should be **HTTP/1.1 301 Moved Permanently**.

Please make sure both versions of the URLs `http://example.com/foo/` and `http://example.com/foo` are behaving as expected. The preferred version should return 200. **The duplicate URL should 301 to the preferred URL.**

## References
 - [To slash or not to slash](https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html)
 - [Optimize your crawling & indexing](https://webmasters.googleblog.com/2009/08/optimize-your-crawling-indexing.html)
 - [Trailing Slashes](https://en.onpage.org/wiki/Trailing_Slashes)
 - [Remove Trailing Slash From the URLs of Your ASP.NET Web Site With IIS 7 URL Rewrite Module](http://www.tugberkugurlu.com/archive/remove-trailing-slash-from-the-urls-of-your-asp-net-web-site-with-iis-7-url-rewrite-module)
