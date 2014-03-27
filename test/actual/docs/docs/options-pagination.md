---
title: options.pagination

area: docs
section: configuration

published: false
---

The `paginate` variable is available at the root of the context. YAML front matter, YAML or JSON are used for configuration, for example:

YAML front matter:

``` yaml
---
title: Portfolio
paginate: 10
---
```



``` hbs
\{{#paginate}}
  \{{paginate-first}}
    \{{paginate-prev}}
      \{{#pages}}...\{{/pages}}
    \{{paginate-next}}
  \{{paginate-last}}
\{{/paginate}}
```
With actual markup it might look like this:
``` html
\{{#paginate}}
<div class="pagination">
  <ul>
    <li><a href="\{{paginate-first}}">First</a></li>
    <li><a href="\{{paginate-prev}}">Prev</a></li>
    \{{#pages}}<li><a href="\{{basename}}\{{ext}}">\{{page.number}} of \{{paginate-length}}</a></li>\{{/pages}}
    <li><a href="\{{paginate-next}}">Next</a></li>
    <li><a href="\{{paginate-last}}">Last</a></li>
  </ul>
</div>
\{{/paginate}}
```
This gives the user the freedom to use whatever markup they require, and to pick and choose the pagination variables they need.

If `paginate` is either undefined or `false` then the `\{{#paginate}}...\{{/paginate}}` block will not be rendered.