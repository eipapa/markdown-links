---
title: Installation

area: docs
section: getting started
---

## Install the "assemble" plugin

This plugin requires Grunt `~0.4.1`

If you haven't used [Grunt](http://gruntjs.com/) before be sure to read the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as how to install and use Grunt plugins.

Then install the plugin with this command:

```shell
$ npm install assemble --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('assemble');
```

When completed, you'll be able to run the various `grunt` commands available


## The "assemble" task

```js
assemble: {
  options: {
    assets: "path/to/assets",
    data:   "path/to/config.json"
  },
  project: {
    options: {
      layout: "path/to/default-layout.hbs",
      partials: "path/to/partials/**/*.hbs"
    },
    files: {
      'dest': ["path/to/pages/**/*.hbs"]
    }
  }
}
grunt.loadNpmTasks('assemble');
grunt.registerTask('default', ['assemble']);
```

### add "grunt-newer" to speed up builds

We also highly recommend that you install [grunt-newer](https://github.com/tschaub/grunt-newer), a must-have task that tells grunt to run tasks against only the files that have been modified since the previous build.

```js
grunt.loadNpmTasks('assemble');
grunt.loadNpmTasks('grunt-newer');

grunt.registerTask('default', ['newer:assemble']);
```


## Grunt.js Options
Following is a brief exerpt from the Grunt.js wiki, please see [Grunt.js docs](http://gruntjs.com/configuring-tasks) for more information. Grunt.js offers far more functionality than what we reference here.

Inside a task configuration, an `options` property may be specified to override built-in defaults.  In addition, each target may have an `options` property which is specific to that target.  Target-level options will override task-level options.

The `options` object is optional and may be omitted if not needed.

```js
grunt.initConfig({
  concat: {
    options: {
      // Task-level options may go here, overriding task defaults
    },
    foo: {
      options: {
        // "foo" target options may go here, overriding task-level options
      }
    },
    bar: {
      // No options specified; this target will use task-level options
    }
  }
});
```

### [Building the Files Object Dynamically](http://gruntjs.com/configuring-tasks#files)

**From [Gruntjs.com: Configuring Tasks](http://gruntjs.com/configuring-tasks#files)**

When you want to process many individual files, a few additional properties may be used to build a files list dynamically. These properties may be specified in both "Compact" and "Files Array" mapping formats.

* `expand` Set to `true` to enable the following options:
* `cwd` All `src` matches are relative to (but don't include) this path.
* `src` Pattern(s) to match, relative to the `cwd`.
* `dest` Destination path prefix.
* `ext` Replace any existing extension with this value in generated `dest` paths.
* `flatten` Remove all path parts from generated `dest` paths.
* `rename` This function is called for each matched `src` file, (after extension renaming and flattening). The `dest` and matched `src` path are passed in, and this function must return a new `dest` value.  If the same `dest` is returned more than once, each `src` which used it will be added to an array of sources for it.

[grunt-target]: (http://github.com/gruntjs/grunt/)


## Related info

* [variables][built-in-variables]
* [Options][]
* [Methods][methods]


#### [Next →][built-in-variables]


<!-- JSON-LD markup -->
<script type="application/ld+json">
{
  "@context" : "http://schema.org",
  "@type" : "SoftwareApplication",
  "name" : "Installation",
  "url" : "https://github.com/assemble/assemble/",
  "publisher" : "ASSEMBLE",
  "applicationCategory" : "getting started",
  "downloadUrl" : "https://github.com/assemble/assemble/archive/master.zip"
}
</script>
