---
title: Embeding shiny into a blogdown post
author: Mehmet Dogan
date: '2023-01-27'
slug: Embeding-shiny-into-a-blogdown-post
categories: ["R"]
tags: ["shiny", "blogdown", "R"]
---

In this post I will walk you through how I embedded a shiny application into this post. This website generated using blogdown package. By embedding an interactive shiny app into a post allows users to interact page and also make the concept easier to understand for them.

I tried to answer to to:
1. Is it possible to embed a shiny application into a post?
2. If yes, is it possible make it responsive?
3. If yes again, what is the easiest way to make it?

### Is it possible to embed a shiny application into a post
I found that this is possible using iframe 


### Is it possible make it responsive
Yes, that is possible using css

I followed [this tutorial](https://www.w3schools.com/howto/howto_css_responsive_iframes.asp) to make it responsive suing css.



### What is the easiest way to make it
Hugo definitely makes our life very easy here. All I had to do is to create a shortcode, e.g., shinyapps.html, under layout/shortcodes folder, place my css code there together with iframe and call it in this document.



{{< shinyiframeresponsive "https://plootra.com/shiny/apps/hello/">}}

You can follow the two-step instructions to to create your own custom shortcode and reuse it in your posts.


1. Create shinyapp.html file under layout/shortcodes direcotry

```css
<style>
.container {
  position: relative;
  overflow: hidden;
  width: 100%;
  padding-top: 56.25%; /* 16:9 Aspect Ratio
  (divide 9 by 16 = 0.5625) you can use other
  aspect ratios as well*/
}

/* Then style the iframe to fit in the container
div with full height and width */
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
  <iframe class="responsive-iframe" 
  frameborder="no" src={{ .Get 0 }}></iframe>
</div>
```

2. Place the shortcode, shinyapp, created in step 1 to markdown file (basically your post).



This is the hugo documentation for custom shortcodes
https://gohugo.io/templates/shortcode-templates/


Also you can watch this tutorial. It gives a very good introduction to custom shortcodes in Hugo. 
{{< youtube Eu4zSaKOY4A >}}



