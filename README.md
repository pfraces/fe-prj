fe-prj
======

Modular build system for front end projects.

Inspired by [ngbp][1] this project provides a basic directory tree and a plugin
system producing cleaner projects with a flexible directory layout.

featuring
---------

*   build system for debug and release environments through
    [grunt][2] tasks
*   front end components managed with [bower][3]
*   plugin system with a curated registry of utilities
*   `index.tpl.html` template that includes all js and css when processed
*   version control with [git][4]

directory tree
--------------

The build system is based on three steps each with its own directory to
operate:

```
/
|- src   (development)
|- build (debug)
|- dist  (release)
```

*   `src/`: Is the place for assets, scripts, templates and all the files that
    will become part of the application.
	
*   `build/`: Is auto-generated by the build system when the `grunt build`
    task is executed. All files and directories in `src/` are copied here. 
    Template files (`*.tpl.*`) are processed as grunt templates	and saved
    without the `.tpl` part. Other templates like `less` or	`coffeescript`
    can be processed here using plugins (see below).

*   `dist/`: Is auto-generated by the build system when the `grunt compile`
    task is executed. Sources become minified and compressed, ready for
    production environments.

Being auto-generated, `build/` and `bin/` directories are ignored by git.

There are other directories not implied directly with the build system:

```
/
|- node_modules
|- bower_components
```

*   `node_modules/`: project management libs, mainly grunt plugins.
*   `bower_components/`: application libs like `angular`, `jquery`, etc.

The dependencies are downloaded through `grunt update` task which is an alias
of `npm update && bower update`. Because of that, `node_modules` and
`bower_components/` are also ignored by git.

Other directories can be added to the root of the project like `docs/` or
`test/`. Plugins can also create their own. By default, these additional
directories will be versioned under git, being part of the project but ignored
by the build system without being part of the app.

plugins
-------

*   `angular`: provides the library and some useful tools
    *   `ui-router`: replaces `<ng-include>` with nested views
    *   `ng-annotate`: generates `$inject` annotations even for `ui-router`
*   `freddie`: static server with proxies and fixtures
*   `eslint`: modular linting support
*   `docco`: provides great documentation through markdown comments in code

[1]: https://github.com/ngbp/ngbp
[2]: https://github.com/gruntjs/grunt
[3]: http://bower.io/
[4]: http://git-scm.com/
