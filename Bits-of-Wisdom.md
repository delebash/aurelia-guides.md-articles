#### Summary

This page is a collection of brief explanations / advices of lot less depth than you could find at <http://blog.durandal.io/2015/02/03/aurelia-qa/> for example. This comes as the consequence that Aurelia Guides is the resource written by Aurelia Developers for Aurelia Developers and its purpose is to **augment** -- **not replace** [Aurelia official documentation][1].

* * *
* * *


#### 1\. jspm package manager fails to find the npm module I need.

**Context Section**
Aurelia requires the use of **jspm** (see **[this](http://blog.aurelia-guides.com/2015/08/28/aurelia-and-jspm/)** for more information) and jspm is designed to load any "package" from either jspm registry, github and npm registry. This short article describes some less than happy experience in pursuing that goal with a specific package from npm registry that I used a lot in my "Angular days".

* * * 

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
* * *


#### 2\. Should I write my apps using TypeScript or ES6?

**Context Section**
Aurelia applications can be written either in "plain" ES6 Javascript or TypeScript - and this question is often asked by many

 
See the **[answer][11]** provided by **Mike Graham**, introduced by **Rob Eisenberg**

* * *

After reading this blog post and being concerned about the all popular view that only TypeScript will prevent you from digging yourself a hole too deep to bail yourself out of - I asked Mike this same question in the context of "my app will be too big to be written JavaScript" issue.

"Stay with ES6 if you are comfortable with it" - was Mike's brief reply and I knew that he was pointing out that ES6 is a very different animal from today's ES5. So, at least for now, I am staying with ES6 :-)

* * *
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

