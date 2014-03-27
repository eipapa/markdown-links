---
title: Pages

area: docs
section: templates
---

## Rendering Pages

### Excluding pages

**From the YAML Front Matter of a page**

You may exclude files from being rendered by adding `published: false` to the YAML Front Matter of a page.

```yaml
---
title: Just testing some stuff on this page, it should not be published
published: false
---
```

**From the Gruntfile**

Exclude files from being rendered by prefixing source file patterns with `!`. Visit the Grunt.js docs to [learn more about globbing](http://gruntjs.com/configuring-tasks#globbing-patterns) patterns.

##### [Quoted from the Grunt.js docs](http://gruntjs.com/configuring-tasks#globbing-patterns) →

```javascript
// All files except for bar.js, in alpha order:
{src: ['foo/*.js', '!foo/bar.js'], dest: ...}

// All files in alpha order, but with bar.js at the end.
{src: ['foo/*.js', '!foo/bar.js', 'foo/bar.js'], dest: ...}
```


## Related info

{{#draft}}* [Pages Arrays][pages-arrays]{{/draft}}
{{#draft}}* [Pages Collections][pages-collections]{{/draft}}
* [handlebars-helpers][handlebars-helpers]
