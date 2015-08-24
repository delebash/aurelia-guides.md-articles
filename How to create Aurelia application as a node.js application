### Introduction

At the moment, everyone has seen / run / analyzed the Aurelia [Skeleton Navigation](https://github.com/aurelia/skeleton-navigation) application and many &quot;newbies&quot; used it as a starting point for their own application development.

Most people with more than casual interest, discovered that this app is started as a `gulp serve` [task](https://github.com/aurelia/skeleton-navigation/blob/master/build/tasks/serve.js), defined as

        var gulp = require(&amp;#39;gulp&amp;#39;);
        var browserSync = require(&amp;#39;browser-sync&amp;#39;);

        // this task utilizes the browsersync plugin
        // to create a dev server instance
        // at http://localhost:9000
        gulp.task(&amp;#39;serve&amp;#39;, [&amp;#39;build&amp;#39;], function(done) {
          browserSync({
            open: false,
            port: 9000,
            server: {
              baseDir: [&amp;#39;.&amp;#39;],
              middleware: function (req, res, next) {
                res.setHeader(&amp;#39;Access-Control-Allow-Origin&amp;#39;, &amp;#39;*&amp;#39;);
                next();
              }
            }
          }, done);
        });

So, this app as currently packaged at Github, does not use any back-end -- it is launched by [BrowserSync](http://www.browsersync.io/) instead.

Well, Aurelia framework is a front end tool, with highest degree of flexibility I have seen so far. I believe that there is a lot of interest among Application developers planning to use Aurelia who would like to see examples of how to make Aurelia Node.js be the back end, since this is probably the most likely to be used back end (see **[this](http://blog.modulus.io/top-10-reasons-to-use-node)** for list of reasons even if these arguments were written before Aurelia&#39;s birthday))

This blog posts (from the Back End Development category) analyses the brilliantly composed [Node version](https://github.com/zewa666/aurelia-node) of the same Navigation Skeleton app written by core-team member Vildan Softic, known as `zewa666`. As a consequence of this choice, Vildan features as the first Aurelia core team member writing for **[this blog](http://blog.aurelia-guides.com/)**.

* * *

[thumbs-rating-buttons]

* * *
