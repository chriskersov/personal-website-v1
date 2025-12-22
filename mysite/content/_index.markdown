---
title: Home
---

[<img src="https://simpleicons.org/icons/github.svg" style="max-width:15%;min-width:40px;float:right;" alt="Github repo" />](https://github.com/yihui/hugo-xmin)

# Chris Kersov

## Data Science in E-Mobility at Shell <img src="https://logos-world.net/wp-content/uploads/2020/11/Shell-Emblem.png" alt="Shell logo" style="max-height:1.3em; display:inline-block; vertical-align:text-bottom; margin-left:-0.4em; margin-bottom: 0.1em" />

BSc (Hons) Computer Science and Artificial Intelligence at University of Bath

<!-- make the image link to my github -->
<!-- i want to draw a cool image like https://nicholassobolev.com/ -->
<!-- i should have a section about university and university modules and coursework -->
<!-- have those pdfs that prove i am a student -->
<!-- link the uni in the line above -->

<!-- ## Data Science in E-Mobility at Shell <img src="https://wepoweryourcar.com/wp-content/uploads/Shell-Recharge-Public-Charging-Network-Guide.png " alt="Shell logo" style="max-height:10em; vertical-align:middle; " /> -->

Currently on placement year doing data science within E-Mobility at Shell.
Studying Computer Science and Artificial Intelligence at the Univeristy of Bath.
Playing tennis, table tennis, badminton, padel. Solving Rubik's cubes of all various shapes and sizes: 2x2, 3x3, 4x4, 5x5, pyraminx, megaminx. Doing my best to learn mandarin. Travelling when I can. trying Trying hard to take cool photos. Eating a lot. I've always wanted to document my life. Maybe I can start with blogs, perhaps one day I will start posting vids on youtube.

<!-- can have a page about speedsolving along with my best time and maybe a solve as well -->
<!-- Include a page about travel with photos I am proud of.  -->

```bash
find . -not -path '*/exampleSite/*' \( -name '*.html' -o -name '*.css' \) | xargs wc -l
```

```
      12 ./layouts/single.html
      20 ./layouts/list.html
      13 ./layouts/terms.html
       5 ./layouts/404.html
       0 ./layouts/_partials/foot_custom.html
       0 ./layouts/_partials/head_custom.html
       9 ./layouts/_partials/footer.html
      20 ./layouts/_partials/header.html
      51 ./static/css/style.css
       7 ./static/css/fonts.css
     137 total
```

I can certainly further reduce the code, for example, by eliminating the CSS, but I believe a tiny bit of CSS can greatly improve readability. You cannot really find many CSS frameworks that only contain 50 lines of code.

Although it is a minimal theme, it is actually fully functional. It supports pages (including the home page), blog posts, a navigation menu, categories, tags, and RSS. With [a little bit customization](https://github.com/yihui/hugo-xmin/blob/master/exampleSite/layouts/_partials/foot_custom.html), it can easily support LaTeX math expressions, e.g.,

`$${\sqrt {n}}\left(\left({\frac {1}{n}}\sum _{i=1}^{n}X_{i}\right)-\mu \right)\ {\xrightarrow {d}}\ N\left(0,\sigma ^{2}\right)$$`

All pages not under the root directory of the website are listed below. You can also visit the list page of a single section, e.g., [posts](/post/), or [notes](/note/). See the [About](/about/) page for the usage of this theme.
