
# Factory JavaScript Style Guide

Our primary rules for writing JavaScript stem from [Google's JavaScript Style Guide][gsg] and the guidelines set by a configuration file for [JSLint][lint]. While you may not like all of these rules, they work well and help establish consistency across multiple development teams.

This is a working guideline and may change over the course of time.


## Style Guide Links

The following links provide guidelines and information on writing squeaky clean `.js` files. They are ordered in importance as to who you should listen to first.

- [JSLint Options][lint-options] (see below for more information)
- [Google's Style Guide][gsg]
- [Crockford's Style Guide][crockford]


## Factory Style Guide Addendum

The following addendum rules either override the guidelines or define new ones where they are not listed in the above links. Anything written here trumps all others.


### Document Settings

- Use spaces instead of tabs
- Indentation is 2 spaces
- Avoid lines longer than 80 characters
- Use newlines to group logically related pieces of code

### Comments

- Be meaningful but not verbose
- Comments shouldn't be a replacement for code readability
- Remember tests, specs, features are documentation in itself
- Use [JSDoc][jsdoc] style for documenting (follow [Google's guidelines][gsg])


### Naming

Naming schemes should be descriptive about what the object contains or actions it will perform.

#### Files

Should be lower case and words should be separated by a dash (`-`). JavaScript test or spec files should have either a trailing `_test` or `_spec` prefixed by the file name they are testing against.

    modal-video-gallery.js
    modal-video-gallery_test.js
    modal-video-gallery_spec.js


#### Packages

Nouns or gerunds (the -ing noun form of a verb).

    controls
    logging


#### Variables, Constants, Properties, Classes

Nouns. Separate variables, properties and constant words with an underscore "`_`" and intercaps for Classes with the first letter capitalized.

    var dog; // variable
    var pink_dog; // variable

    var SPEED_X; // constant

    var BlueShoes = function () { // class
      var delta_x = 100; // property
    };

We leave it up to the developer on whether they chain variable initializations separated by commas. If you are doing this, make sure to align the indentation.


    function initialize() {
      var dog = 'Mansfield',
          good_beer = 'St. Ides',
          x = 12;
    }


For readability sake, please don't one line these.

    function initialize() {
      // this will get your teeth kicked in..
      var dog = 'Mansfield', good_beer = 'St. Ides', x = 12;
    }


#### Functions, Methods, Handlers

Verbs. Use intercaps with the first letter lower case. Functions should do one thing and one thing well. Where possible functions should `return` the action it is performing.

When building views we generally use the following function names: `initialize`, `build`, `show`, `hide` and anything that can be cleaned up will have the function or method name `dispose`. Subroutines of these functions may then be something like `initializeBubbles`, `buildBubbles`, `showBubbles`, `hideBubbles`, `disposeBubbles`.

##### Functions:

    function initialize() {
      // body...
    }

    function buildBubbles() {
      // body...
    }

    var object = {
      initialize: function () {
        // body...
      },

      buildBubbles: function () {
        // body...
      }
    };


##### Methods:

    BlueShoes.prototype.initialize = function () {
      // body...
    };

    BlueShoes.prototype.buildBubbles = function () {
      // body...
    };

    BlueShoes.prototype = {

      initialize: function () {
        // body...
      },

      buildBubbles: function () {
        // body...
      }
    };


##### Event Handlers:

Event handlers should be named by concatenating "Handler" to the type of event:

    function mousemoveHandler(e) {
      // body...
    }


### Semicolons

Always use Semicolons. Relying on implicit insertion can cause subtle, hard to debug problems. Don't do it. You're better than that. This becomes really apparent when minimizing. Listen to JSLint, it will not steer you wrong.

### Quotes

Use single quotes for JavaScript strings and double quotes for HTML. This makes it dead simple when writing HTML inline so you don't have to escape those silly little characters.

    var native_string = 'using single quotes';

    var html_string = '<div id="radness" class="monkeys"></div>';


## JSLint Configuration Settings

Our settings in [JSLint][lint-options] may piss you off, but there in place for a good reason. [JSLint][lint-options] runs with the configuration options below on the CI box.

    var options = {

      adsafe     : false, // if ADsafe should be enforced
      bitwise    : true,  // if bitwise operators should not be allowed
      browser    : true,  // if the standard browser globals should be predefined
      cap        : false, // if upper case HTML should be allowed
      css        : false, // if CSS workarounds should be tolerated
      debug      : false, // if debugger statements should be allowed
      devel      : true,  // if logging should be allowed (console, alert, etc.)
      eqeqeq     : true,  // if === should be required
      evil       : false, // if eval should be allowed
      forin      : false, // if for in statements must filter
      fragment   : false, // if HTML fragments should be allowed
      immed      : true,  // if immediate invocations must be wrapped in parens
      laxbreak   : false, // if line breaks should not be checked
      newcap     : true,  // if constructor names must be capitalized
      nomen      : false, // if names should be checked
      on         : false, // if HTML event handlers should be allowed
      onevar     : false, // if only one var statement per function should be allowed
      passfail   : false, // if the scan should stop on first error
      plusplus   : true,  // if increment/decrement should not be allowed
      regexp     : true,  // if the . should not be allowed in regexp literals
      rhino      : false, // if the Rhino environment globals should be predefined
      undef      : true,  // if variables should be declared before used
      safe       : false, // if use of some browser features should be restricted
      sidebar    : false, // if the System object should be predefined
      strict     : false, // require the "use strict"; pragma
      sub        : false, // if all forms of subscript notation are tolerated
      white      : true,  // if strict whitespace rules apply
      widget     : false, // if the Yahoo Widgets globals should be predefined
      indent     : 2,     // set the expected indentation level

      // the names of predefined global variables:
      // the following are defined by frameworks such as nodejs, jasmine, jQuery, Prototype

      predef     : ['exports',
                    'module',
                    'require',
                    'process',
                    '__filename',
                    '__dirname',
                    'GLOBAL',
                    'describe',
                    'it',
                    'expect',
                    'asyncSpecDone',
                    'asyncSpecWait',
                    'window',
                    'jQuery',
                    '$',
                    '$$',
                    'Event',
                    'Class',
                    'Element']
    };


## JSLint Editor Support

The CI box runs [nodelint][nodelint] and within that repositories [wiki][nodelint-wiki] is a list of Editors that support it. MK has a [TextMate Bundle][mate] and will work on MacVim and RubyMine integrations shortly.

You can always run [nodelint][nodelint] from the command line. See MK for installation instructions.


[gsg]: http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml
[crockford]: http://javascript.crockford.com/code.html
[lint]: http://www.jslint.com/
[lint-options]: http://www.jslint.com/lint.html
[flex]: http://opensource.adobe.com/wiki/display/flexsdk/Coding+Conventions
[jasmine]: http://pivotal.github.com/jasmine/
[jsdoc]: http://code.google.com/p/jsdoc-toolkit/
[nodelint]: http://github.com/tav/nodelint
[nodelint-wiki]: http://github.com/tav/nodelint/wiki/Editor-and-IDE-integration
[mate]: http://github.com/mkitt/nodelint.tmbundle
