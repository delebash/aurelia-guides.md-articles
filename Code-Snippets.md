Code snippets are organized in the form of a Q&A document, where questions are typically in the form "how to I do this in Aurelia".

Code snippets need some contextual information in order to be of any value, so each snippet is preceded by the **Context section**. Most of the snippets published in **Aurelia-Guides** originate from the Gitter Chat Room [Aurelia /  Discuss](https://gitter.im/Aurelia/Discuss) which has a large "membership" consisting of mostly Aurelia "newbies" asking for advice. More experienced developers answering these questions are most often the authors of these snippets and they use **[ScribeFire](https://chrome.google.com/webstore/detail/scribefire/elkkomimknapgodalnkjeddkjnjkfmfp)** Chrome extension as the tool to publish their answers together with the question.

* * *
* * *

#### How to render different view structures in Aurelia?

**Context Section**
_To Be Written_

I have a common html structure in my app.html in order to apply for all pages:

    <template>
    <require from="header"></require>
    <require from="side-bar"></require>
    <require from="theme-panel"></require>
    <require from="footer"></require>
    <!-- BEGIN HEADER -->
    <js-header></js-header>
    <!-- END HEADER -->

    <div class="clearfix"></div>

    <!-- BEGIN CONTAINER -->
    <div class="container">
        <div class="page-container">
            <!-- BEGIN SIDEBAR -->
            <js-side-bar></js-side-bar>
            <!-- END SIDEBAR -->
            <div class="page-content-wrapper">
                <div class="page-content">
                    <!-- BEGIN STYLE CUSTOMIZER(optional) -->
                    <js-theme-panel></js-theme-panel>
                    <!-- END STYLE CUSTOMIZER -->
                    <!-- BEGIN ACTUAL CONTENT -->
                    <div class="fade-in-up">
                        <router-view></router-view>
                    </div>
                    <!-- END ACTUAL CONTENT -->
                </div>
            </div>
        </div>
        <!-- BEGIN FOOTER -->
        <js-footer></js-footer>
        <!-- END FOOTER -->
    </div>
    <!-- END CONTAINER -->
    </template>

However, in my case, i have a login page with a totally different structure compared to others. In my app.js, i tried to use getViewStrategy() method to control which views i will render as following:

    activate(params, routeConfig, navigationInstruction){
        this.navigationInstruction = navigationInstruction;
        //console.log("params", params); // undefined
        //console.log("routeConfig", routeConfig); // undefined
        //console.log("navigationInstruction", navigationInstruction); // undefined
        //console.log("router", router); //undefined
    }
    getViewStrategy(){
        if(this.navigationInstruction == 'login'){
            return "app_login.html";
        } else {
            return "app.html";
        }
    }

in the code above, 'navigationInstruction' is undefined. Therefore, my solution cannot work well. Does anybody have another solution? Thanks so much!

##### Answer 

Great question. In fact, when you have two totally sections of the same single page application, the right thing to do is create multiple root view models, or shells.

First, set your app up for custom initialization by adding ``aurelia-app="main"`` to your body tag, and creating a new initialization file correspondingly named ``main.js``. It should look like this.  

    export function configure(aurelia) {
      aurelia.use
        .standardConfiguration()
        .developmentLogging();

      // notice that we are setting root to 'login'
      aurelia.start().then(app => app.setRoot('login'));
    }

The ``app.setRoot('login')`` line tells Aurelia to load a file called ``login.js`` as the app root. This file should look similar to your current ``app.js``. You can do anything you want in this file and it's corresponding view, and it will stay totally separate from your main app.

To navigate back to your main app, you'll need to call ``app.setRoot('app')``, which means you'll need to inject the Aurelia object into your Login view model.

    import { inject, Aurelia } from 'aurelia-framework';

    @inject(Aurelia)
    export class Login {
      constructor(aurelia) {
        this.aurelia = aurelia;
      }
      goToApp() {
        this.aurelia.setRoot('app');
      }
    }

Answer provided by [Matthew James Davis](http://stackoverflow.com/users/1981050/matthew-james-davis) - see the full write-up here: [Aurelia Login Best Practices](http://www.foursails.co/blog/aurelia-login-best-practices-pt-1/)