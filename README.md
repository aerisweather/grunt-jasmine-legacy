grunt-jasmine-legacy
=================

A Grunt task for running Jasmine v1.3 tests using RequireJS and PhantomJS.


# Why not use [grunt-contrib-jasmine](https://github.com/gruntjs/grunt-contrib-jasmine)?

The [grunt-contrib-jasmine](https://github.com/gruntjs/grunt-contrib-jasmine) task has [dropped support for Jasmine v1.3](https://github.com/gruntjs/grunt-contrib-jasmine/commit/c755025c577af6383b8eba754ea8cf542a084d74). I created this task for a project with a large base of tests written using the Jasmine v1.3 API.

# How does it work?

The grunt-jasmine-legacy task:

* Uses a [template](src/templates/specrunner.html.tmpl) to create an AMD spec runner
* Executes the spec runner using [`PhantomJS`](http://phantomjs.org/)
* Reports the results using the [`PhantomJSReporter`](src/helpers/phantomjsreporter.js), which listens to events emitted by [grunt-lib-phantomjs](https://github.com/gruntjs/grunt-lib-phantomjs)
* Saves the spec runner HTML file for further debugging, if needed (using the standard `jasmine.HTMLReporter`)


# Example configuration

```javascript
'jasmine-legacy': {

  // Each sub-task will have a specrunner created for it
  // eg /tests/specrunner-myLib.html
  myLib: {
    options: {

      // Location of require.config settings
      amdConfigModules: [
        '../config-amd'
      ],

      // Additional AMD configuration
      // to apply to the spec runner
      amdConfig: {
        paths: {
          someRealObject: 'someMockObject'
        }
      },

      // Location of Jasmine specs to test
      specs: [
        'tests/**/*.spec.js'
      ],

      // AMD modules required for all tests
      libs: [
        'jasmine',
        'jasmine-console',
        'jasmine-html',
        'lib/myCustomJasmineMatchers',
        'sinon'
      ],

      // Files to not be included as test specs
      exclude: [
        'tests/fixtures/**/*.js'
      ]
    }
  },
}
```