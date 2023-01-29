---
title: How to Embed Shiny Apps Into a blogdown Post
author: Mehmet Dogan
date: '2023-01-27'
slug: Embeding-shiny-into-a-blogdown-post
categories: ["R"]
tags: ["shiny", "blogdown", "R"]
---

If you have a website or blog and you'd like to embed a shiny app into your content, I will walk you through the steps to achieve it: 

1. How to embed a shiny app into a blogdown post?
2. How to make it responsive?
3. How can we create a custom Hugo shortcode and reuse it in future content? (for Hugo sites only)


Embedding shiny apps into your content allows readers to engage with your content, enabling you to convey your points.

{{< shinyiframeresponsive "https://plootra.com/shiny/apps/hello/">}}


### How to embed a shiny app into a blogdown post?
It's possible to embed it using an ***iframe*** tag. An iframe, also known as Inline Frame, is an element that loads another HTML element inside of a webpage. In our case, another HTML element is the shiny app. 

You can insert the following HTML code into your post. It will place the shiny app on your blog post when you publish it.

```
<iframe height="100%" width="100%" frameborder="no" src="url-to-shiny-app"> </iframe>
```

"URL-to-shiny-app" should be the entire path to the app. It must start with http or https. It can be your app deployed in some server or can be someone else's app.

You can modify the height, width, and frameborder attributes to change the app's look.

You can embed a shiny app and other elements, such as external ads, videos, or other interactive components, into the page using an iframe tag.

One problem with this solution is that the embedded app may look awkward if your readers visit your site from their mobile phones. So let's move to the next section to determine how we can make it responsive.



### How to make it responsive?

Using CSS code, you can make your shiny app responsive.

I used the below CSS to make the shiny app responsive. [This tutorial](https://www.w3schools.com/howto/howto_css_responsive_iframes.asp) helped me understand how to make an *iframe* responsive using CSS.

Place CSS code and iframe tag into the body of the post, and it will be responsive.

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
  <iframe class="responsive-iframe" frameborder="no" src="URL-to-shiny-app"></iframe>
</div>
```



### How can we make a custom Hugo shortcode and reuse it in future content? (for Hugo sites only)

Here comes the power of Hugo! It makes our life easier. If you are already using Hugo and unfamiliar with the shortcodes, please visit the below Hugo documentation and tutorial.


The Hugo documentation for custom shortcodes: https://gohugo.io/templates/shortcode-templates/

By the way, I embedded this video also using Hugo's shortcode :smile:
{{< youtube Eu4zSaKOY4A >}}


The benefit of this solution is you can reuse it in your future content. You can accomplish it in a two-step process.

1. Make a shortcode

Create an HTML file, e.g., shinyapps.html, under the /layout/shortcodes directory. Then you need to put the **CSS code** and **iframe tag** into the shinyapps.html file.

![Hugo layout folder](C:/Users/ploot/OneDrive/R/plootra/static/hugo_layout_folder.png)


The content of the shinyapps.html
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
  <iframe class="responsive-iframe" src={{ .Get 0 }}></iframe>
</div>
```


You will use the filename before html extension as a shortcode name. 

2. Use the following syntax to place the shortcode into the markdown file (your post).

![shinyapp shortcode](C:/Users/ploot/OneDrive/R/plootra/static/shinyapps.png)


