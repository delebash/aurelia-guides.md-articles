### Summary

Aurelia-Guides Snippet Manager is a tool that **assist in clipping &quot;parts&quot; of information exchange** between participants in [Aurelia chat room](https://gitter.im/Aurelia/Discuss) and storing that information at [Aurelia-Guides](http://aurelia-guides.com/) (site currently under the construction)

* * *

The following exchange between @vcardins and @vcardins (yes, he provided the answer to his own question):

> What is the the best way to cancel a routing and redirect to another route? I got it by doing

    this.ea.subscribe(&amp;#39;router:navigation:processing&amp;#39;, (payload:any) =&amp;gt; {
          if (payload.instruction.config.name == &amp;#39;login&amp;#39; &amp;amp;&amp;amp; isAuth) {
            this.router.navigate(&amp;#39;dashboard&amp;#39;);
          }
        })
    `&lt;/pre&gt;&gt; answering my own question:
    &lt;pre&gt;`authorizeStep.ts
    ...
    run(routingContext, next) {
        if (routingContext.nextInstruction.config.name == &amp;#39;login&amp;#39; &amp;amp;&amp;amp; this.authProvider.isAuthenticated) {
          return next.cancel(new Redirect(this.appSettings.defaultRoute));
        }
        if (routingContext.nextInstructions.some(i =&amp;gt; i.config.auth)) {
          if (!this.authProvider.isAuthenticated) {
            return next.cancel(new Redirect(this.appSettings.loginRoute));
          }
        }
        return next();
      }
    ...

* * *

[thumbs-rating-buttons]

* * *

My primary candidate for this tool (_thank you Dan for the tip_) was [GistBox Clipper](http://www.gistboxapp.com/) which looks as created to be Aurelia-Guides Snippet Manager. Unfortunately, after a few hours of using it and checking other people&#39;s opinion I found that:

It has several nasty bugs, the worst of which was that the click on Start a new gist button

  ![](http://blog.aurelia-guides.com/wp-content/uploads/2015/08/startanewgist.png)</img>

has completely unpredictable outcome - mostly of the type &quot;nothing happens&quot; :-)

This is of course sufficient to drop this candidate, however I also found that this app is classified as a PUP (potentially unwanted program) - see [this](http://www.malwarekillers.com/ads-by-gistbox-clipper-removal/) as an example.

I will evaluate two alternatives (_again, thank you Dan_) and look for more, as I believe @teslan&#39;s evaluation:

> I think that the gitter channel is extremely important to the core team because it gives them live feedback on what they are doing well and what they can improve on. However, as the channel grows it starts for them to be more like picking needles from a haystack. Hence, Aurelia-Guides - the haystack reducer.
