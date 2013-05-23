# Happy Plan! [![Build Status](https://travis-ci.org/kud/happy-plan.png?branch=master)](https://travis-ci.org/kud/happy-plan)

> When Grunt.js uses Jekyll as a peon.

Happy plan is a static website generator based on a bundle of amazing tools . It's just all about fun.

### What in it?

* A static website generator from html or markdown: [Jekyll](https://github.com/mojombo/jekyll).
* A task-based command line build tool: [Grunt.js](http://gruntjs.com/) & some pre-defined tasks (scripts, styles & images automatic minification & compression).
* An amazing CSS pre-processor, [Sass](http://sass-lang.com/) directly served with [Compass](http://compass-style.org/).
* A quick way to provide scalable icons as font thanks an awesome Grunt task [grunt-webfont](https://github.com/sapegin/grunt-webfont).
* A [Livereload](http://livereload.com/) server ([tiny-lr](https://github.com/mklabs/tiny-lr) provided by the [grunt-contrib-livereload](https://github.com/gruntjs/grunt-contrib-livereload) task) to make development as fast as hell.
* A package manager for the web called [Bower](https://github.com/twitter/bower) to handle web components.

Oh, by the way, why "happy plan" ? [Here is not the answer](http://www.youtube.com/watch?v=5zVVKXT8Vi0).

## Arborescence

    .
    ├── bin                             // Some binaries used by happy plan
    │   ├── newpost.js                  // Allows you to create a new post via $ node ./bin/newpost.js
    │   └── publish.sh                  // To publish on gh-pages via $ ./bin/publish.sh
    ├── build                           // Where your app is built but you don't have to care about it
    ├── dist                            // Your final app
    ├── src                             // This is where all comes
    │   ├── _config                     // Everything about config
    │   │   └── config.yml              // Configure jekyll
    │   ├── _layouts                    // Layouts
    │   │   ├── default.html            // The layout called by default
    │   │   └── post.html               // A layout which calls default and adds some markups
    │   ├── _pages                      // Your pages which will be at the root of the project
    │   │   ├── feed.xml                // RSS page
    │   │   └── index.html              // Main page
    │   ├── _partials                   // Elements you can call everywhere in your pages (it's the jekyll _includes folder)
    │   ├── _posts                      // Posts for blog
    │   │   └── _drafts                 // Posts you don't want to publish
    │   ├── assets                      // All about design
    │   │   ├── _components             // Folder for bower elements
    │   │   ├── _images                 // Design images
    │   │   ├── _scripts                // JS
    │   │   │   └── script.js           // a JS file
    │   │   ├── _styles                 // CSS
    │   │   │   ├── _font-icons.scss    // Used if you use grunt-webfont (svg-to-font tool), do not edit it
    │   │   │   └── style.scss          // Where you put all your styles
    │   │   ├── _glyphicons           // SVG transformed into fonts
    │   │   └── fonts                   // Fonts
    │   └── medias                      // Content elements like videos, images, audios
    ├── .bowerrc                        // Where you define your options for bower
    ├── Gruntfile.js                    // Compilation file
    ├── component.json                  // Where you define your options used by bower
    ├── happy-plan.default.json         // All config used by happy plan
    ├── happy-plan.json                 // You can create this file to override the default config.
    └── README.md                       // PLEASE, READ IT, but it seems you are

## TL;DR
According you already have ruby and npm installed.

    $ gem install jekyll compass && npm install -g grunt-cli bower && npm install

## Requirements

The easy way is on **OS X** (but it shouldn't be so hard to make this working on any unix like system. Make a PR :)).

### Jekyll [[+](https://github.com/mojombo/jekyll/wiki/install)]

    $ (sudo) gem install jekyll
    
### Compass [[+](http://compass-style.org/install/)]

    $ (sudo) gem install compass

### Node.js [[+](https://github.com/joyent/node/wiki/Installation)]

    $ brew install node

#### Npm [[+](https://github.com/isaacs/npm)]

    $ curl http://npmjs.org/install.sh | sh

### Grunt.js (>0.4) [[+](http://gruntjs.com/getting-started)]

    $ npm install -g grunt-cli

### Optionals

#### Grunt-Webfont[[+](https://github.com/sapegin/grunt-webfont#installation)]

    $ brew install fontforge ttfautohint
    $ brew install https://raw.github.com/sapegin/grunt-webfont/master/Formula/sfnt2woff.rb

#### Bower [[+](https://github.com/twitter/bower#installing-bower)]

    $ npm install -g bower

### Required for testing

#### Tree [[+](http://mama.indstate.edu/users/ice/tree/)]

    $ brew install tree
---

## Installation

When everything above is okay, just run:

    $ npm install

That's it. Now you can start your website bro'.

### Configuration

You can create a `happy-plan.json` at the root to override the content of `happy-plan.default.json`. Both will be **deeply merged** together.

To configure others used tools, you have differentes possibilities depending on the tool.

#### Bower

Bower configuration file is generated from the `bower.bowerrc` section in the `happy-plan` configuration

#### `/src/_configs/*`

`.hlb` files are [handlebar](http://handlebarsjs.com/) templates parsed by [assemble](https://github.com/assemble/assemble) grunt task where Happy-Plan JSON configuration is available.
You can use edit `hlb` files `/src/_configs/*.hlb` that should be created from `.sample` ones if one doesn't exist.

* **Jekyll**: `_config.yml` is `/src/_configs/jekyll._config.yml.hlb`

* **Compass**: `config.rb` is `/src/_configs/compass.config.rb.hlb`

To generate these 3 configurations files (bower, jekyll & compass) before launching the `dev` task (eg: to install a bower component) you can run

    $ grunt happyPlan:init

*This task is not required since it's launched by all build tasks*

## Build

To build the website

    $ grunt dist

### Development

Using `watch` will allow you to test & dev your posts with livereload included (it needs a [livereload browser extension](http://go.livereload.com/extensions))

    $ grunt

#### Server

When you start `grunt`, you already have a server started to display your webpages. `http://localhost:8080` should be opened in your browser automatically :)

---

## Publish on gh-pages (github)

If you want to publish your build on the gh-pages:

    $ grunt publish

This script builds the website (grunt dist) & commit + push on gh-pages branch.

#### Warning for username.github.com

`username.github.com` is a bit special. Indeed, the `master` branch acts like a `gh-pages` so you have to publish your website on `master` and not `gh-pages` (don't try `gh-pages`, it won't work).

For that, create or modify `happy-plan.json` and add this option:

```
"git": {
    "branch": "master"
  }
```

Now you can easily push your website on this branch via `$ grunt publish`


## Create a new post

Want to create a new post quickly? No problem.

    $ happyPlan newpost

This create a new post in `src/_posts/_drafts`.

For more informations about posts, just read [Jekyll's doc](https://github.com/mojombo/jekyll/wiki)

## Command helper

There is an available `happyplan` binary. You can add `./bin`to your PATH to be able to call this bin directly instead of grunt.

Here is the available commands

Generate required configuration from `happy-plan.json`

    $ happyplan init

Launch the development task (init, build, watch, server & auto open)

    $ happyplan dev

Launch the optimized build for distribution

    $ happyplan dist

## Contributing

When you want to fix a bug or add a feature, just be sure to get all testing requirements installed, & run tests before making your *Pull Request*.

You can run in one command the build process & the tests.

    $ npm test

In case you don't know it yet, `npm {cmd}` just run the command `{cmd}` specified in the `package.json`. In our case, it run `grunt test`. And to be precise, the `test` task run the `dist` task & the `nodeunit` one.

---

## Upgrading version

To get latest stable update you can just merge

    $ git remote add happy-plan git@github.com:kud/happy-plan.git
    $ git pull happy-plan master

To try experimental features, you can just git pull another branch like this

    $ git pull happy-plan feature-x

**When you update from remote be careful to following *Release history* to update if needed you configuration files until we found a simpler solution to handle updates**

## Release History

  * Unreleased   v0.3.0   Update dependencies (Node 0.10 support), add JSHint & Travis-CI, add configurable configuration files, add embed server & auto open in the browser. Also switch Fontcustom for grunt-webfont.
 * 2013-02-02   v0.2.0   Add config file, change folder tree
 * 2013-01-31   v0.1.1   Update to Grunt 0.4
 * 2013-01-29   v0.1.0   Real first release as Happy-Plan

---

## Migrations

[Jekyll already have a migration doc](https://github.com/mojombo/jekyll/wiki/blog-migrations)

Note: For Wordpress, [wordpress-to-jekyll-exporter](https://github.com/benbalter/wordpress-to-jekyll-exporter) seems a quick & good choice (+ keep disqus thread id !)

---

## Support

Come up and say hello on [IRC](http://webchat.freenode.net/?channels=happyplan)! We'll be glad to answer you if you have any questions.

    #happyplan @ irc.freenode.net

