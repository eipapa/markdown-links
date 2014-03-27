---
title: options.pages

area: docs
section: configuration

published: false
---



The way it works is you can create a very simple layout that has only the head and body tags, for example. Other layouts will then use that layout as a base, but with additions such as a navbar, footer etc..

For example:

`base-layout.hbs`

``` html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Document</title>
  </head>
  <body>
    \{{> body }}
  </body>
</html>
```

`kitchen-sink-layout.hbs`

``` html
---
layout: base-layout.hbs
---
\{{> navbar }}
\{{> body }}
```


