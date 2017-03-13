# Zine
Hello! Welcome to Zine, a Jekyll theme. https://jekyllrb.com/docs/home/

Zine is written with an eye toward simple longform layout and art direction to play with fun features in new browsers. It is not at all safe from XSS as you can write code directly into any post, so don't add on any kind of signup function. It's for a closed group of known authors. It's not strict really. If you want to just write plain html you can, markdown, you can, use a GUI, you can. It's made to be usable by non-coder artists, writers, and designers, but not to be annoying for coders. 


A note for less technical users

You can make posts through the user interface. TODO The rest of this ReadMe is about writing files in a text editor and making changes to the code in the site and it is not in the least necessary to read or understand any of it to use Zine. 

-----------------------------------------------

### Layout

It has built in styles for lots of common longform story blocks. The longform.css holds these styles (except for tools). This means things like quote styles, image layouts, dropcaps.
.copy {body text set to a nice width with padding etc}
.splash {a full screen picture - you can change the picture and put headings or quotes etc on top}
.invert {inverts the dark and light}
.parallax {makes that trendy scrolling effect over images}

There are lots - have a look. They all use simple English words and you can add them together and nest them etc to make more complicated layouts. There are ipsummed examples in the posts folder.

### Embedding from other sites

You can embed external content like youtube playlists, sketchfab, soundcloud playlists, tweets, ao3, 8track playlists by pasting in the embed or share codes those sites provide. Or you can use a Liquid include if you prefer.

In Liquid you can embed them by passing in the id as a variable like this:

{% include youtube_playlist.html id="" %}

I will make that available through an extension to Markdown or something I guess.TODO

### Fun toys and tools

Zine uses lots of javascripts. You can call them in the front matter as tools

tools: [slideshow, slider, map, youtube, typeset, timeline, scrollify, animation]

#### Tools List

You can put your own settings in the instances. They are all includes and you can edit them and you can add more. This is the current set of tools:
grid: packery and draggabilly, included by cdn
map: - TODO  - need to generate API key or find open one
slideshow: currently using flexslider, cdn
slider: juxtapose, cdn
scrollify: scrollify, cdn
typeset: slabtext, cdn
animation: prostyle, cdn

If you prefer, you can download these scripts and serve them yourself from the /assets/js/ folder. Be aware that the more scripts you use on a page, the slower your site will be. But you can give yourself as many options as you like as scripts are only called on the pages they are used.

### Looks

Zine allows you to set various looks. Looks are things like custom fonts, page specific style, a hero picture , a legend (that you can set the line breaks on), and a colour scheme.(TODO on scheme)
hero:
legend: |
 <span
fonts: [font, font, font]
colours: []
css: |
resources: |

#### fonts: [Oswald, Muli, Cabin+Sketch]

You can choose any fonts on Google fonts. You can also add your own webfonts but you have to declare those in the custom css field yourself. You can declare any page-specific css and page-specific resources and they will print in the <head>. Put your css in css and your resources (like javascripts) in resources. 

css: |
 #yourcss { property: value }
resources: |
 <script src="/assets/js/example.js"></script>

If you feel ambitious, you can also completely drop any of the site styles by writing them in the front matter:

drop: [main, longform, icons, tools, response]

### Site Pages

#### Index Pages

Index pages show lists of posts or collection items. They are set to draw little posters of each post - calling the information from the looks in the post front matter. This is done by:
1. calling the grid and typesetting tools in the front matter
tools: [grid, typeset]
2. calling the first font in the font list and setting that on the heading

The list items are sized by a class cycle (wide, tall, etc) in the post-list if you want to change the sizing. You need to give the list items a width or the grid and typeset tools won't work properly. Always size the list items first, then run the typesetting js. If you just want them all the same size write uniform: true in the front matter.

#### About Pages

About pages show things like a note from the editor, a contact form, contributors, etc. TODO: about nav
-----------------------------------------------------------------------------

## FRONT MATTER, POSTS

Here are all the things you can set in the front matter. You only need to set the layout, title, author, and category. Everything else is optional.
POSTS
---
layout: post
title: "Title of Post"
authors: [name, name]
categories: [articles, topic]
date: 2017-04-03
classes: [note - this adds classes on the body tag which might make css easier in some cases]
tools: [animation, slideshow, slider, map, youtube, typeset, timeline, scrollify]
hero: hero.jpg
legend: |
 <span>Controlled</span> <span>Heading</span>
fonts: [Oswald, Muli, Amatic+SC]
colours: [#009900, #333333]
resources: |
 <script src="/assets/js/example.js"></script> 
css: |
  .yourcss { property: value }
 
drop: [drop: [main, longform, icons, tools, response]
pitch: |
 If this isn't filled in an automatic excerpt will be generated
---

## FRONT MATTER, PEOPLE
---
name: "Mary Sue"
contributor: true
socials:
- ao3: name
- tumblr: name
..
bio: |
---

----------------------------------------------------------------------------- 

## HOW TO...

### Add a new tool.

Let's add lettering.js and make it available to a post.
1. make a new file in _includes/lettering.html. 
2. Paste the javascript source and instance in to this include. In this case this is
<script src="https://cdnjs.cloudflare.com/ajax/libs/lettering.js/0.7.0/jquery.lettering.min.js"></script>
<script>
$(document).ready(function() {
$(".fancy_title").lettering();
});
</script>
3. Declare it in your post front matter in your tools list. Use the include file name.
tools: [youtube, lettering, scrollify]

### Add a new category index page

The category layout sorts posts by category. To make a new category and generate an index page for it, do this:
1. Make a new file in articles/your-new-category.html
2. In the front matter, write the new category name where the example has your-new-category
---
layout: category
category: your-new-category
title: your-new-category
permalink: /articles/your-new-category/
tools: [grid, typeset]
---
You can add a post to this index page by writing the category in the front matter, after articles:

categories: [articles, your-new-category]

You can add loads of categories if you really want to.

-----------------------------------------------------------------------------

## Themes [not active yet] still vastly TODO

Sassy
The default is written in plain CSS. It's not really highly specified or complicated and it's easy to read if you know CSS at all. But if you prefer SASS, you can choose this theme. It's basically the same except the CSS is split up into little bits, for each story block or tool:
sitewide colours and fonts are set in [looks]
main.css is composed of [core, header, nav, lists, footer]
longform.css is composed of [copy, quotes, images, dimensions, alignment]
tools.css is composed of [grid, slideshow, slider, timeline]


Editions
The default is the single edition zine. If you want to use this to make a magazine with (annual, quarterly, monthly, etc) editions, choose the Editions Theme. It's arranged a little differently.
Front Page:
> Top menu: No topic links as these may differ from edition to edition. 
> Editions grid. In the front matter, uniform is set to true (uniform: true), so it draws regularly shaped magazine covers. 
Edition Page:
-> Same as One Off Front Page
You can set the looks for each edition in that edition front matter. 

Sassy Editions
Editions with SASS.

Megazine
The cute poster layout isn't really suitable for loads and loads of editions. This theme drops that for a more conventional list layout without custom fonts and so on. You can still load custom fonts on any post.

Bombazine
This is a drastically simplifed zine with no looks or tools. Very fast but quite severe.

Publisher
After your zine is completed, you can run [] to export it as an e-book. You can offer it for download and even make available to be printed on demand. There's no checkout system. If you want to charge for your zine you will have to build a checkout yourself.

    



