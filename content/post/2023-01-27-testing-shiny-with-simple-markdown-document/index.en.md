---
title: Testing Shiny with simple markdown document
author: Mehmet Dogan
date: '2023-01-27'
slug: testing-shiny-with-simple-markdown-document
categories: []
tags: []
---

In this post I tried to embed a shiny application into the post. I tried to answer to:
1. Is it possible to embed a shiny application into a post?
2. If yes, is it possible make it responsive?
3. If yes again, what is the easiest way to make it?

### Is it possible to embed a shiny application into a post
I found that this is possible using iframe 


### Is it possible make it responsive
Yes, that is possible using css

I followed the following tutorial to to make it responsive:
https://www.w3schools.com/howto/howto_css_responsive_iframes.asp


### What is the easiest way to make it
This was the most pleasant one. Hugo definitely makes our life very easy here. All I had to do is to create a shortcode, e.g., shinyapps.html, under layout/shortcodes folder, place my css code there together with iframe and call it in this document.



{{< shinyiframeresponsive "https://plootra.com/shiny/apps/hello/">}}

You can find the steps below to create your own custom shortcode and reuse it in your posts.

In shinyapp.html file

```
<style>
.container {
  position: relative;
  overflow: hidden;
  width: 100%;
  padding-top: 56.25%; /* 16:9 Aspect Ratio (divide 9 by 16 = 0.5625) */
}

/* Then style the iframe to fit in the container div with full height and width */
.responsive-iframe {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 100%;
}
</style>


<div class="container"> 
  <iframe class="responsive-iframe" frameborder="no" src={{ .Get 0 }}></iframe>
</div>
```

In this post (a markdown file) you place the short code as described in documentation or video below.





You can find the related hugo documentation for customer shortcodes by visiting:
https://gohugo.io/templates/shortcode-templates/


Also you can watch a very useful tutorial:
{{< youtube Eu4zSaKOY4A >}}



