#### Summary

This article is a collection of brief explanations / advices of lot less depth than you could find at <http://blog.durandal.io/2015/02/03/aurelia-qa/> for example. This comes as the consequence that Aurelia Guides is the resource written by Aurelia Developers for Aurelia Developers and its purpose is to **augment** -- **not replace** [Aurelia official documentation][1].

* * *

#### 1\. JSPM fails to find the npm module I need.

Few days back, I wanted to create a sample of an Aurelia application which uses **[Stormpath Authentication and Authorization services][2]** (this sample is a part of a larger **[Aurelia Security Services][3]** article still under development).

As I prefer to start "from scratch" in the "experiment phase", I took the approach described in the document [Smallest Aurelia Application - created from scratch][4]. **Knowing** that I need [Official Stormpath SDK for Node.js][5] library, distributed via **[npm][6]**, and knowing further that I have to use **[jspm][7]** (package manager for [System.js module loader][8]) to load a package from npm registry into the Aurelia **[ES6][9]** world, the thing to do is simple

1.  Create my "[Smallest Aurelia Application][4]".
2.  Run `jspm install stormpath`

Well, instead of getting my app configured to have the access to Stormpath module, I got this:

    λ jspm install stormpath
    
    warn Running jspm globally, it is advisable to locally install jspm via npm install jspm --save-dev.
    
    Package.json file does not exist, create it? [yes]:y
    Would you like jspm to prefix the jspm package.json properties under jspm? [yes]:y
    Enter server baseURL (public folder path) [./]:y
    Enter jspm packages folder [y\jspm_packages]:y
    Enter config file path [y\config.js]:y
    Configuration file y doesn&amp;#39;t exist, create it? [yes]:
    Enter client baseURL (public folder URL) [/]:
    Do you wish to use an ES6 transpiler? [yes]:
    Which ES6 transpiler would you like to use, Babel or Traceur? [babel]:
         Updating registry cache...
    
    err  Repo jspm:stormpath not found!
    
    warn Installation changes not saved.
    
Does npm registry contain stormpath module? Yes, of course - as shown below
    
    λ npm install stormpath
    stormpath@0.10.2 node_modules\stormpath
    ├── njwt@0.0.1
    ├── jwt-simple@0.2.0
    ├── flat@1.6.0
    ├── deep-extend@0.4.0
    ├── underscore@1.5.2
    ├── async@0.7.0
    ├── node-uuid@1.4.3
    ├── redis@0.12.1
    ├── properties-parser@0.2.3
    ├── underscore.string@2.3.3
    ├── glob@3.2.11 (inherits@2.0.1, minimatch@0.3.0)
    ├── request@2.40.0 (forever-agent@0.5.2, aws-sign2@0.5.0, stringstream@0.0.4, oauth-sign@0.3.0, tunnel-agent@0.4.1, json-stringify-safe@5.0.1, qs@1.0.2, mime-types@1.0.2, form-data@0.1.4, http-signature@0.10.1, tough-cookie@2.0.0, hawk@1.1.1)
    ├── moment@2.8.4
    └── memcached@0.2.8 (hashring@0.0.8, jackpot@0.0.6)
    
Why did  my search for stormpath fail? Well, sometimes it is good to read the documentation **very carefully**. Had I done this, I would know that instead of  ``jspm install stormpath`` I should have written ``jspm install npm:stormpath``

* * *

#### 2\. Should I write my apps using TypeScript or ES6?

See the **[answer][11]** provided by **Mike Graham**, introduced by **Rob Eisenberg**

After reading this blog post and being concerned about the all popular view that only TypeScript will prevent you from digging yourself a hole too deep to bail yourself out of - I asked Mike this same question in the context of "my app will be too big to be written JavaScript" issue.

"Stay with ES6 if you are comfortable with it" - was Mike's brief reply and I knew that he was pointing out that ES6 is a very different animal from today's ES5. So, at least for now, I am staying with ES6 :-)

* * *

 [1]: http://aurelia.io/docs.html
 [2]: http://stormpath.com
 [3]: http://blog.aurelia-guides.com/category/security/
 [4]: http://blog.aurelia-guides.com/2015/08/22/smallest-aurel…d-from-scratch
 [5]: https://www.npmjs.com/package/stormpath
 [6]: https://www.npmjs.com/
 [7]: http://jspm.io/
 [8]: https://github.com/systemjs/systemjs
 [9]: http://es6-features.org/
 [10]: http://javascriptplayground.com/blog/2014/11/js-modules-jspm-systemjs/
 [11]: http://blog.durandal.io/2015/05/06/getting-started-with-aurelia-and-typescript/

####3. How to render different view structures in Aurelia?

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