---
title: Interests
# author: Chris Kersov
---

<br>

<h1 style="font-size:3.5rem; margin:0 0 -0.2em;">Interests</h1>

<br>

ideas for future projects

- UK weather analysis

- create an npm package that converts mpo file to two jpegs

- aus open predictor
- roland garros predictor (so many further things that can be built on top of this)
- world cup predictor
- premier league predictor

- an f1 related project

- llm free tier memory mover

- terminal typing test with basic customisability that dies when you make a mistake
- but has better versions as well
- and also gives in depth analsis as to waht you did while typing

- quant finance related projects
- something that could be useful for my final year project
- with some machine learning could be cool

- make my github profile look pretty

- make a readme for my github main page

- look into how best to market projects to get users. like for the 3ds one for example.

- a project that takes your current chat lets say you reached your limit then converts it to some format. then you take that to a new free ai tier then upload it there and boom its caught up and dont need to worry about the context window. what format to convert it to and how i am not sure. binary, tokens, idk. also how can you export a whole chat. im sure thats possible. but yeah this should be a useable tool maybe even a chrome extension or something.

- just had an idea to evolve the ML grand slam predictor further
- i want to have live match prediction kinda like google and football
- use this video to learn how to do this ml stuff by looking a match:
  - https://www.youtube.com/watch?v=L23oIHZE14w
- just cool to be able to learn and play with this stuff anyways
- but perhaps the ml predictor could make a prediction
  - then after the match is over watch the match back and improve its prediction or something
- idk im not exactly sure yet but there is something cool that can be done here i know there is

- i want to do the ml predictor for mens and woman
- perhaps for aus open i can do for mens only
- then for roland garros i can do for woman as well
- i also want to have money involved
- what about sentiment analysis
- also what bookies
  - haha what if you make a parlay for some likely combinations

- need to fix the pronounciation of chris kersov to be able to work on all browsers
- just make it play a stored audio

- have a cv download on the first page

### Sports:

#### Tennis

Talk about tennis history.
How much I love it.
How long I have been playing.
My equipment, shoes etc.
Predictions for next grand slam.
ML predictor for next grand slam github link maybe.
(I could do this for each year and then see how evolves etc).
Racket stringing as sort of a mini business.
IMAGE OF ME PLAYING TENNIS - NEEDS TO BE COLD.

#### Table tennis

Talk about how much I love table tennis.
My equipment.
How I got into table tennis.
Watching table tennis and fav players etc: ma long, truls, anders, fan.
My fav ma long photo and maybe truls celebration photo.
IMAGE OF ME PLAYING TABLE TENNIS AT WORK.

#### Badminton

Talk about my badminton interests.
How I got into it.
Want to play more, will play more at uni.
My equipment.
IMAGE OF ME PLAYING BADMINTON WITH YU SUM.

#### Padel

### Interests:

#### Rubik's Cubes:

Solving Rubik's cubes of various shapes and sizes:
2x2, 3x3, 4x4, 5x5, pyraminx, megaminx.

#### Learning Mandarin:

Give some explanation as to why I am learning Mandarin.
How much I have learnt so far.
My learning goals: HSK 1 etc.

#### Travelling:

Recently started travelling more.
Absolutely love it.
Places I have been to: list them.
Places I plan and want to go.

#### Photography:

Some cool photos I have taken.
I wish to learn more about photography.
I love taking photos of pretty scenery.

#### Eating:

I love eating.

#### Learning:

Learning in my spare time.
What stuff am I interested in learning.
Books I am reading for personal learning. HOML.
Any courses I am taking.

#### Anime:

Anime I am watching currently.
Animes I have enjoyed.
Could include some manga panels or cool photos.

#### Gaming:

Minecraft.
Nintendo 3DS jailbroken.

#### Personal Finances:

Interested in staying on top of my finances.
Created Excel spreadsheet to track.
Could link the sheet.

#### Tech:

Logitech MX master 3.
M4 Macbook Air.
iPad air something (i want to look into e ink tablets).
Sony xm5s (cant live without them).
Nintendo 3ds.
logitech mx master keyboard
or my own keyboard I created (show photos - blank keycaps)

Want to purchase and upgrade a thinkpad
and use linux

also rewrite cv in latex or typst. can also have it previewed in one of the pages. with some annotations or something maybe idk.

it could be cool to have my timezone and current time for me as well. also have the hk timezone on there.

i want something about my philosophy towards life as well.

also i want to enable google analytics.

when you tab and then it higlights the surrounding of links i want that to be customised. i want the scroll bar to be customised as well.

I managed to make code blocks with syntax highlighting. I could make something cool where like it shows a block of code or like a function of sorts and then an animted output of like a cool graph or something. my github profile hahahhaha

perhaps on my projects page i could have a heatmap of my leetcode
and also a heatmap of my github

```python
print("hello world")
```

```
 > hello world
```

i can also render latex equations qhich is cool. maybe i might find a use for this somewhere. maybe when talking about what i am learning idk.

$$
{\sqrt {n}}\left(\left({\frac {1}{n}}\sum _{i=1}^{n}X_{i}\right)-\mu \right)\ {\xrightarrow {d}}\ N\left(0,\sigma ^{2}\right)
$$

looks like i can link to other parts just by doing this [posts](/post/) [notes](/note/). but idk what these pages are. in the template yihui mentions these 'pages not under the root directory' and shows these. so this must be something to do with the footer.

i also want to improve the footer.

i have realised that what i mean by footer and header are the things above and below the dotted lines. but these arent header.html and footer.html. i need to improve my understanding

**XMin** is the first Hugo theme I have designed. The original reason that I wrote it was I needed a minimal example of Hugo themes when I was writing the [**blogdown**](https://github.com/rstudio/blogdown) book. Basically I wanted a simple theme that supports a navigation menu, a home page, other single pages, lists of pages, blog posts, categories, tags, and RSS. That is all. Nothing fancy. In terms of CSS and JavaScript, I really want to keep them minimal. In fact, this theme does not contain any JavaScript code at all, although on this example website I did introduce some JavaScript code (still relatively simple anyway). The theme does not contain any images, either, and is pretty much a plain-text theme.

The theme name "XMin" can be interpreted as "**X**ie's **Min**imal theme" (Xie is my last name) or "e**X**tremely **Min**imal theme".

## `hugo.yaml` (the config file)

For this example site, I defined permalinks for two sections, `post` and `note`, so that the links to pages under these directories will contain the date info, e.g., `https://xmin.yihui.org/post/2016/02/14/a-plain-markdown-post/`. This is optional, and it is up to your personal taste of URLs.

```yaml
permalinks:
  note: "/note/:year/:month/:day/:slug/"
  post: "/post/:year/:month/:day/:slug/"
```

You can define the menu through `menu.main`, e.g.,

```yaml
menu:
  main:
    - name: Home
      url: ""
      weight: 1
    - name: About
      url: "about/"
      weight: 2
    - name: Categories
      url: "categories/"
      weight: 3
    - name: Tags
      url: "tags/"
      weight: 4
    - name: Subscribe
      url: "index.xml"
```

Alternatively, you can add `menu: main` to the YAML metadata of any of your pages, so that these pages will appear in the menu.

The page footer can be defined in `.Params.footer`, and the text is treated as Markdown, e.g.,

```
params:
  footer: "&copy; [Yihui Xie](https://yihui.org) 2017 -- {Year}"
```

Here `{Year}` means the year in which the site is built (usually the current year).

## Custom layouts

There are two layout files under `layouts/_partials/` that you may want to override: `head_custom.html` and `foot_custom.html`. This is how you inject arbitrary HTML code to the head and foot areas. For example, this site has a file `layouts/_partials/foot_custom.html` to support LaTeX math via KaTeX and center images automatically:

```html
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/katex/dist/katex.min.css" />
<script
  src="//cdn.jsdelivr.net/combine/npm/katex/dist/katex.min.js,npm/katex/dist/contrib/auto-render.min.js,npm/@xiee/utils/js/render-katex.js"
  defer
></script>

<script
  src="//cdn.jsdelivr.net/npm/@xiee/utils/js/center-img.min.js"
  defer
></script>
```

You can certainly enable highlight.js for syntax highlighting by yourself through `head_custom.html` and `foot_custom.html` if you want.

If you do not like the default fonts (e.g., `Palatino`), you may provide your own `static/css/fonts.css` under the root directory of your website to override the `fonts.css` in the theme.

## Other features

I could have added more features to this theme, but I decided not to, since I have no intention to make this theme feature-rich. However, I will teach you how. I have prepared several examples via pull requests at https://github.com/yihui/hugo-xmin/pulls, so that you can see the implementations of these features when you check out the diffs in the pull requests. For example, you can:

- [Enable Google Analytics](https://github.com/yihui/hugo-xmin/pull/3)

- [Enable Disqus comments](https://github.com/yihui/hugo-xmin/pull/4)

- [Enable highlight.js for syntax highlighting of code blocks](https://github.com/yihui/hugo-xmin/pull/5)

- [Display categories and tags on a page](https://github.com/yihui/hugo-xmin/pull/2)

- [Add a table of contents](https://github.com/yihui/hugo-xmin/pull/7)

- [Add a link in the footer of each page to "Edit this page" on Github](https://github.com/yihui/hugo-xmin/pull/6)

To fully understand these examples, you have to read [the section on Hugo templates](https://bookdown.org/yihui/blogdown/templates.html) in the **blogdown** book.

# Design philosophy

Lastly, a few words about my design philosophy for this theme: I have been relying on existing frameworks like Bootstrap for years since I'm not really a designer, and I was always scared by the complexity of CSS.

When I started writing this theme, I asked myself, "_What if I just write from scratch?_" No Bootstrap. No Normalize.css. I don't care about IE (life could be so much easier without IE) or inconsistencies among browsers (for personal websites). As long as the theme looks okay in Chrome, Firefox, and Safari, I'm done. Thanks to the simplicity of Markdown, you cannot really produce very complicated HTML, and I think styling the HTML output from Markdown is much simpler than general HTML documents. For example, I do not need to care much about form elements like textareas or buttons.

After I finished this theme, I started to wonder why I'd need `normalize.css` at all. The default appearance of modern browsers actually looks pretty good in my eyes, after I tweak the typeface a little bit.

Compared to inconsistencies across browsers, I care much more about these properties of HTML elements:

- Tables should always be centered, and striped tables are easier to read especially when they are wide. Tables should not have vertical borders.
- An image should be centered if it is the only child element of a paragraph.
- The `max-width` of images, videos, and iframes should be `100%`.

I hope you can enjoy this theme. The source code is [on Github](https://github.com/yihui/hugo-xmin). Happy hacking!
