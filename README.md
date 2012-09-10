# One Web/Mobile First Responsive Boilerplate


## What is it? 

The One Web Frontend Boilerplate is a modular framework for building responsive 
websites with Apache Server Side Includes: http://httpd.apache.org/docs/2.2/howto/ssi.html.

It draws code from many other projects, combining various solutions into a custom, 
modular frontend framework (please see Credits section below). The project also 
includes Ant build script that runs code quality tools against JavaScript and 
CSS files, minifying and concatenating them at the end of the process. 

There's nothing really new in this boilerplate, but it works well for me which is 
why I'm publishing it here for you to use and improve. It builds on many of the 
best practices found in the resources listed under Credits. It basically extends 
popular boilerplates, including 320 and Up (https://github.com/malarkey/320andup/), 
HTML5 Boilerplate (http://html5boilerplate.com/), and Mobile Boilerplate 
(http://html5boilerplate.com/html5boilerplate.com/dist/mobile/) and many others, with 
Server Side Includes. The goal is to achieve a modular and responsive frontend 
build environment, following industry best practices. The framework can easily be 
plugged into Continuous Integration solutions, such as Jenkins: http://jenkins-ci.org. 

This framework doesn't include any grid. You decide how you build your site. 
If you need a grid though, have a look at the Fluid Grid: http://akikoo.github.com/Fluid-Grid/. 
If you need a good set of LESS utilities, see 320 and Up: https://github.com/malarkey/320andup/.


## File structure

### There are two main directories: /build and /webroot.

* /build contains Ant build script and all the tools you need to make your 
    frontend build. Common build properties are defined in /build/config/project.properties. 
    There's also a folder called masterpage, which is used as a blueprint for creating new pages. 

* /webroot contains two subdirectories: /assets and /html. 

* /webroot/assets contains all the LESS files, stylesheets, JavaScript files and 
    theme images. 

* /webroot/html contains all the HTML files, generated by Apache Server Side Includes. 
    HTML properties are defined in /webroot/config.shtml.

Dev files are in /webroot/assets and /webroot/html.
Optimised files are in /build/publish/assets and /build/publish/html.


## Build tools

* Java Development Kit (JDK) (http://www.oracle.com/technetwork/java/javase/downloads/index.html)
* Ant (http://ant.apache.org/)
* Ant-Contrib Tasks (http://ant-contrib.sourceforge.net/)
* YUI Compressor (http://developer.yahoo.com/yui/compressor/)
* Rhino (http://www.mozilla.org/rhino/)
* JSLint (http://www.jslint.com/)
* JSHint (http://www.jshint.com/)
* CSSLint (http://csslint.net/)
* HTML Compressor (http://code.google.com/p/htmlcompressor/)
* JSDoc Toolkit (http://code.google.com/p/jsdoc-toolkit/)
* JsDoc Toolkit Ant Task (http://code.google.com/p/jsdoc-toolkit-ant-task/)
* Closure Compiler (https://developers.google.com/closure/compiler/)
* r.js optimizer (http://requirejs.org/docs/download.html#rjs)
* less-rhino (https://github.com/cloudhead/less.js/blob/master/dist/less-rhino-1.1.5.js)
* OptiPNG http://optipng.sourceforge.net/
* jpegtran http://www.ijg.org/


## Environment setup

### Apache Ant

* Whether you're on Windows or Mac, you'll need the Java Development Kit (JDK) 
    (at least version 1.4). You can download it here: 
    http://www.oracle.com/technetwork/java/javase/downloads/index.html. 
    If you're not sure which version of the JDK you have, run the command 
    java -version in the terminal.

* Download Apache Ant here (on Mac OSX it's usually already installed): 
    http://ant.apache.org/bindownload.cgi. On Windows, it's probably best to extract 
    the contents of the zip to C:\ant.

* See this article for how to finish the installation on your platform:
    http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/ 
    (see section Windows- and Mac-Specific Install Bits.)

### Apache SSI
To permit SSI on your server, see this article: 
http://httpd.apache.org/docs/2.2/howto/ssi.html

All the other tools needed in the local build are in the tools folder.

### Build configuration
After Apache Ant and SSI setup, you need to do two more things to configure the build:

1. In /build/config/project.properties, look for 'web.home' in line number 121. 
    Change the path to your local directory.
2. In that same file, look for 'web.url' in line number 123. Create an Apache 
    virtualhost that points to the location you defined for 'web.home' above. 

You should now be up and running with both the environment and the local build. 


## Things you need to know

* A CSS preprocessor, LESS (http://lesscss.org/) is used to compile the stylesheets. 
    If you don't want to use a preprocessor, you can of course work with the CSS 
    files directly. To do so, remove &lt;css.compile.less /&gt; macrodef call in /build/build.xml.

* Media Queries are based on 16px default font size and defined in ems. 
    If you don't go for responsive design (you should!), just replace the default 
    @import rules in /webroot/assets/less/styles-nomq.less with your own modular 
    ones. The framework is designed to be modular so you should split the rules 
    into logical modules, and place the styles in /webroot/assets/less/modules. 

* JavaScript should not be relied on for layout. That's why I've adopted a 
    bulletproof solution from Nicholas Zakas and Tantek Çelik: 
    http://www.nczonline.net/blog/2011/03/22/using-html5-semantic-elements-today/, 
    http://tantek.com/presentations/2010/11/html5-now/.

* Don't use IDs in CSS selectors. Use classes, or ARIA landmark roles instead 
    (referenced with CSS attribute selectors). See also http://oli.jp/2011/ids/.

* I'm using Sticky footer solution: http://www.cssstickyfooter.com.


## Logic

### HTML
* Each page has a controller in /webroot/html/pages/pagename/index.shtml. 
    In that file, we include the config file and set variables, define the view, 
    and template file that we need to include, to render that particular page. 
    For more information, see project main index file: 
    https://github.com/akikoo/one-web-boilerplate/blob/master/webroot/html/index.shtml

### CSS - six stylesheets by default, compiled by LESS, included in the following order: 
* /webroot/assets/css/common/normalize.css (reset styles)
* /webroot/assets/css/common/base.css (global, mobile first styles, containing only 
    common colour and typographic rules for basic experience to all users)
* /webroot/assets/css/common/utilities.css (helper styles from HTML5 Boilerplate and 
    HTML5 Mobile Boilerplate)
* /webroot/assets/css/common/theme.css (temp theme styles, you should create your own)
* /webroot/assets/css/styles-mq.css (layout with Media Queries for responsive, 
    enhanced design for smartphones, tablets and larger screens)
* /webroot/assets/css/styles-nomq.css (layout without Media Queries for legacy 
    IE 6/7/8 browsers; alternatively, you can use this as non-responsive main 
    stylesheet that simply includes modular stylesheets). 

styles-mq.less and styles-nomq.less are the main stylesheets that @import all the 
common styles. Note that styles are @import-ed only for development. For production, 
the build script inlines and minifies styles in the same order that you @import-ed 
them. Nice, eh? But keep in mind that you have to @import the core styles (see above) 
before anything else. 

If you need to overwrite common rules, or add new ones on a page level, you can do 
so by creating a new stylesheet in /webroot/assets/less/pages. Page specific stylesheet 
must have the same name than the page that uses it. This way the page specific 
stylesheet is automatically included in the template, as well as minified for 
deployment. 

So you basically have two possible main routes here: go responsive, or go modular 
(or preferably both). Keep in mind that if you work with LESS, you should only do 
changes in /webroot/assets/less/ directory, as the files in /webroot/assets/css/ 
will obviously be the generated ones, rewritten on each save or build. 

New stylesheets you create should probably be placed in /webroot/assets/less/modules. 
Remember to add @import rules for any new styles in styles-mq.less and styles-nomq.less. 
After the base styles, the order in which the module stylesheets are included 
should't matter (you write your styles carefully, right?) The idea is that module 
styles inherit only from base rules, not from other modules. 

### JavaScript
* Third-party plugins are included in /webroot/assets/js/lib. Custom scripts are 
in /webroot/assets/js/modules. Dependancies are managed by RequireJS (http://requirejs.org/), 
a script loader that supports AMD (Asynchronous Module Definition) API. Script paths 
and their dependencies are defined in /webroot/assets/js/config.js. Scripts are 
imported in /webroot/assets/js/main.js. 


## Credits

### Boilerplates:
* http://html5boilerplate.com
* http://html5boilerplate.com/mobile
* http://stuffandnonsense.co.uk/projects/320andup/
* Big thanks to *Will Howat* (@willhowat: http://twitter.com/willhowat) and *Andrew 
    Massey* (@wearymadness: http://twitter.com/wearymadness) for the inspiration, 
    code, and fresh ideas. Great work on the Archetype framework!

### Generic build/deploy process optimization:
* Thanks to *Dennis Green-Lieber* (@dennislieber: http://twitter.com/dennislieber) 
    for promoting the use of the framework and for great suggestions and ideas for 
    making it better. 

### Solutions:
* http://code.google.com/chrome/chromeframe/
* http://www.cssstickyfooter.com/

### Media queries:
* http://forabeautifulweb.com/blog/about/hardboiled_css3_media_queries/
* http://stuffandnonsense.co.uk/blog/about/proportional_leading_with_css3_media_queries/
* http://www.blog.highub.com/mobile-2/revisit-hardboiled-css3-media-queries/
* http://css-tricks.com/6731-css-media-queries/
* http://www.quirksmode.org/blog/archives/2010/08/combining_media.html
* http://www.slideshare.net/bryanrieger/rethinking-the-mobile-web-by-yiibu
* http://www.cloudfour.com/css-media-query-for-mobile-is-fools-gold/
* http://www.broken-links.com/2011/02/21/using-media-queries-in-the-real-world/
* http://nicolasgallagher.com/mobile-first-css-sass-and-ie/

### Inspiration:
* http://www.abookapart.com/products/responsive-web-design
* http://easy-readers.net/
* http://www.alistapart.com/articles/responsive-web-design/
* http://www.lukew.com/ff/entry.asp?933
* http://adactio.com/journal/1716/
* http://adactio.com/journal/4780/
* http://adactio.com/journal/1700/

### Markup:
* http://www.456bereastreet.com/archive/201103/html5_sectioning_elements_headings_and_document_outlines/
* http://www.456bereastreet.com/archive/201104/html5_document_outline_revisited/
* http://mezzoblue.com/archives/2011/01/31/boilerplate/
* http://www.nczonline.net/blog/2011/03/22/using-html5-semantic-elements-today/
* http://tantek.com/presentations/2010/11/html5-now/
* http://microformats.org/wiki/hatom

### Images:
* http://unstoppablerobotninja.com/entry/fluid-images/
* http://www.cloudfour.com/responsive-imgs-part-2/

### CSS:
* http://oli.jp/2011/ids/
* http://code.google.com/p/universal-ie6-css/
* https://github.com/necolas/normalize.css

### JavaScript:
* http://requirejs.org/
* https://github.com/tbranyen/backbone-boilerplate
* https://github.com/ryanfitzer/Example-RequireJS-jQuery-Project


## Ant build process

### To build your project, do the following

This assumes you've set up the build, as explained in Build configuration.

1. Open terminal and go to /path_to_your_project/build 
2. Run ant -buildfile build.xml

### The sequence of events is then as follows: 

1. Old build directory called /publish is deleted
2. /publish directory is recreated, and build timestamps are added as text files
3. HTML header and footer files are edited, to include minified and concatenated 
    assets, created during the build
4. SHTML snippets are called to generate full HTML web pages
5. SHTML snippets are called to generate HTML modules 
6. SHTML file extensions are changed to HTML and all pages are copied to 
    build/publish/html. Compressed HTML versions are copied to 
    build/publish/html-compressed
7. Component, module, page and template lists are generated, to be included in 
    the project root index page
8. HTML header and footer files are reverted, to include separate assets again 
    (we'll continue developing!)
9. LESS files are compiled to CSS files
10. CSSLint tool is run against all CSS files (however excluding third-party stylesheets)
11. JSHint tool is run against JavaScript code (excluding third-party scripts)
12. JSDoc documentation is created and placed in build/publish/docs/jsdocs
13. CSS files are concatenated by inlining all @import-ed styles, producing two 
    files: styles-mq.css and styles-nomq.css (one with and one without Media 
    Queries). This way, we can keep the CSS rules separate from the actual Media 
    Queries. Both files are then minified and placed in build/publish/assets/css. 
    Page specific stylesheets are minified individually.
14. JavaScript files are minified and concatenated and placed in 
    /build/publish/assets/js/lib (currently only Modernizr and require.js.) 
    Note that compiled require.js contains the original require.js and all the 
    modules, loaded with almond require/define shim.
15. Unoptimised images are copied to /build/publish/assets/img
16. Temporary directory that was used during the build is deleted
17. That's it!

Congratulations! You now have a brand new /build/publish directory that has the 
following four directories: 

* HTML files (/build/publish/html), 
* Compressed HTML files (/build/publish/html-compressed), 
* Minified and concatenated CSS and JS files (/build/publish/assets), and 
* JSDoc documentation (/build/publish/docs/jsdocs). 

You can now deploy the site using your favourite Continuous Integration server. 
It could be Jenkins (http://jenkins-ci.org) or Bamboo 
(http://www.atlassian.com/software/bamboo/). You decide. 


## To-Do: 
* Small tweaks here and there...

Thanks and good luck! 

> There's no mobile, everything's mobile.