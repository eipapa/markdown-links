---
title: Some Tutorials
something: <%= _.readJSON("package.json") %>
word: <%= _.uppercase(title) %>
else: <%= _.expand(something) %>
posts: ['README.md']
---
{{! MASTHEAD
================================================== }}
<header class="masthead subhead">
  <div class="container">
    <div class="row">
      <div class="col col-lg-6">
        <h1> {{ uppercase title }} </h1>
      </div>
    </div>
  </div>
</header>
<div class="container">
  <div class="panel panel-docs">
    {{else}}
    <h1> {{ word }} </h1>

    {{#each posts}}
    <h2>{{md this}}</h2>
    {{/each}}
  </div>
</div>