---
layout: post
title: "Testing express with mocha"
date: 2014-04-16 06:13:11 -0700
comments: true
categories: NodeJS, Express
---
Even though this post doesn't technically have anything to do with Mocha, I'm
mentioning it in the title because I was using Mocha, but Mocha has a gap of
features when it comes to testing http interactions. You need to augment it
with another module.

I'm working with NodeJS and trying to experiment creating
a web backend that will handle form posts from my simple html web page. In
order to test the simple express app I wanted to use mocha.

After installing mocha and express I created my handler but wanted a way to
fake the requests. I couldn't fiqure out how to test the application so I
started googling to see what was recommended. I found a post on
[wrecker](http://devcenter.wercker.com/articles/languages/nodejs/getting-started-express-and-mocha.html)
showing to use supertest.

I then started to look to make sure that supertest is
in fact the right tool that I need. I couldn't find a definitive direction on
how to test web form requests using node so I'm posting this.

I confirmed simply by [reviewing code from the one of the nodejs contributors](https://github.com/koajs/statsd/commit/2d22eeee009eff704f2ba2da36be0c50991f3530)
and confirmed that he is using supertest to test their http interactions.
``` javascript
var assert = require('assert');
var request = require('supertest');
var app = require('../server.js');

describe('Post', function() {
 describe('Sunny path', function() {
   it('should just work', function(done) {
      request(app)
      .get('/status')
      .expect(/Hello there!/, done);
   });
 });
});
```
here's the result

{% img /images/mocha_pass.png %}
