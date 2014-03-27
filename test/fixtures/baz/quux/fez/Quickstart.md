---
title: Quickstart

area: docs
section: getting started
---

> Assemble your first site in 5 minutes or less. Are you ready?!

The fastest way is to use [grunt-init-assemble](https://github.com/assemble/grunt-init-assemble),
but if you prefer to start from scratch then this is for you.

We should be able to get your first site running in just a few minutes if:

  1. You are familiar with using `npm` to install packages
  2. You have `npm` and `grunt-cli` installed globally

That just about covers it, so let's get started!

## Setup

### 1. git clone assemble

```shell
git clone https://github.com/assemble/assemble.git "my-project"
```
then

```shell
cd my-project
```

### 2. Install necessary packages

```shell
npm i
```

### 3. Build

```shell
grunt assemble
```

If everything builds properly, then run:

```shell
grunt test
```

And all tests should pass.


### 4. Time to customize!

Ideally, you should start with a nice clean Gruntfile and a brand new `src` directory, but this is a great way to start learning by example. If you get stuck or need inspiration, just head over to [Assemble's documentation](http://assemble.io), or take a look at [some other examples](https://github.com/assemble/assemble-examples).

Have fun!


#### Also see [Resources][resources] →