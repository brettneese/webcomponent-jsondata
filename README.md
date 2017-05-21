# webcomponent-jsondata

This is a simple + fun [WebComponent](https://www.webcomponents.org/) that allows you to simply and easily pull data from any JSON-powered web API into the text of a webpage (as a `<span>` element, actually). I made it because I was writing a paper and I wanted to include view count data pulled from the YouTube API at on the client-side in a Jekyll-powered page, but I imagine there are lots of great uses for it. API-powered blog posts FTW.

You can also optionally replace/parse data before it appears using regexes. It doesn't, for the sake of simplicity, support any other data format other than JSON, and it doesn't know natively about URL encoding or query parameters or OAuth tokens or POST or... but as long as you can GET the data from a URL-encoded, stable URL and have access to the HTML for your page, you can simply include the appopriate <link> tag in your `<head>` (either download `index.html` or get it from a CDN: https://cdn.rawgit.com/brettneese/webcomponent-jsondata/tree/0.1/index.html. If you use the CDN, please use a tagged version so a push to `master` doesn't accidentally break evetything) and a `<json-data>` element with the attributes explained below in your body and it will fill in your page with the appropriate data when it is loaded.

I assume it only works on Chrome because that's the only place I tried it but the Polymer polyfill is included so it should be fine elsewhere.

## Attributes:

- `url` (string, required) - a URL-encoded, stable, URL to get the JSON from. If you need query paramters, add them at the end.
- `path` (string, required) - a [JSONPath selector](http://goessner.net/articles/JsonPath/) to select the data in the object. For instance, `"$.items.0.statistics.viewCount"`
- `regex` (string, optional) - a regex to use for finding data to replace. No leading or following slashes. For instance, `(\d)(?=(\d\d\d)+(?!\d))`  
- `replace` (string, optional) - the pattern to replace the regex matches with. For instance, `$1,`
- `regexMode` ('i', optional, default: 'g') - if you want the regex to only match the first instance set this to `'i'`

## Example:

```
<head>
  <link rel="import" href="https://cdn.rawgit.com/brettneese/webcomponent-jsondata/tree/0.1/index.html">
</head> 

<body> 

  This video has <json-data url="https://www.googleapis.com/youtube/v3/videos?part=statistics&id=qXY5NIbSFRw&key=YOUTUBE_API_KEY_HERE-9k7U" path="$.items.0.statistics.viewCount" regex="(\d)(?=(\d\d\d)+(?!\d))" replace="$1,"></json-data> views.

</body>
```

### Example Output (as of the time of the readme):

This video has 1,814,851 views. 

(The regex are what gives the numbers their appopriate formatting, at least for US-based audiences. Localization would be nice but I think it's outside of the scope of this library, because I wanted to be able to do general-purpose text manipulation without a bunch of extra attributes.)

## FAQ:

### Does this work on Jekyll/GitHub Pages? 

Yes! 

### Does this work on Medium?

No, Medium won't let you do custom inline HTML. Sad reacts only.

### Can I include this element in a Markdown file?

Probably. Markdown allows you to add plain ol' HTML per the spec. But your parser might not like it.

### Is this heavily tested/error caught/bug free?

No. Probably not. I whipped it up quite fast. I'm surprised I'm bothering to write a readme.

### Is this on Bower?

Ewww.

Maybe someday it will be. See above about how I wrote it really fast.

### What post were you writing that inspired this?

I'm still finishing it up. It's quite a disaster right now. Like I often stop mid sentence or even mid-wor...

### Pull requests?

Are def welcome.

## I have another question/want to contact you! 

brett@neese.rocks

Or Twitter: [@brettneese](https://twitter.com/brettneese)



