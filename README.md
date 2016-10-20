# error-list
Errors and messages seen in console, and their solutions

## Webpack build

- `WARNING in viz.ui.tags.min.js from UglifyJs
   Dropping unused function ...`
   
   > havent added 3rd part library that is being imported to the `external` property in my webpack.dist file
   
# Karma / Webpack
- `ERROR [karma]: { [Error: no such file or directory]
     code: 'ENOENT',
     errno: 34,
     message: 'no such file or directory',
     path: '/_karma_webpack_/views/Foo/Foo.js' }
   Error: no such file or directory
   `
   
   > needed to get out of the karma_webpack folder
   
   ie
   
   ` 
      preprocessors: {
     '../**/test/*Test.js': ['webpack'],
     '../**/Foo.js': ['webpack', 'coverage'],
   },
   `
   
## Angular / webpack

- ` [HMR] Cannot apply update. Need to do a full reload! `


- ` bootstrap a40e730…:25 GET http://localhost:8080/a40e7300d99baba23b78.hot-update.json 404 (Not Found) `



- ` angular.js:13642Error: [$compile:tpload] Failed to load template:  `

    > forgot to change `templateUrl` to `template` in the directive

- `   Uncaught Error: [$injector:modulerr] Failed to instantiate module demoApp due to:
      Error: [$injector:modulerr] Failed to instantiate module {} due to:
      Error: [ng:areq] Argument 'module' is not a function, got Object 
   `
  
  
- ` angular.js:13642Error: [$injector:unpr] Unknown provider: vizUiDataGridTemplateServiceProvider <- vizUiDataGridTemplateService <-       vizUiDataGridController `
    > forgot to add the template.service script to module script
- component does load/blank page/ empty browser
    > needed to add `"window.jQuery":jquery` to 
    ` new webpack.ProvidePlugin({
            $: "jquery",
            jQuery: "jquery",
            'window.jQuery': "jquery"
        })
      ` in the webpack.make\
      
- ` Argument 'fn' is not a function, got string `

      > `.config() and/or `.run()` were named
       ie config('appAppConfig', appAppConfig) 
       
      They expect a single argument only, function or array, and shouldn't be named


## NPM / Node

- ` npm ERR! Windows_NT 6.1.7601
   npm ERR! argv "C:\\Program Files\\nodejs\\node.exe" "C:\\Program Files\\nodejs\\node_modules\\npm\\bin\\npm-cli.js" "install" "--verbose"
   npm ERR! node v5.10.0
   npm ERR! npm  v3.8.3
   npm ERR! code EREADFILE

   npm ERR! Error extracting C:\Users\collsl\AppData\Roaming\npm-cache\fs\0.0.0\package.tgz archive: ENOENT: no such file or directory, open 'C:\Users\collsl\AppData\Roaming\npm-cache\fs\0.0.0\package.tgz' `
   
   >problem with fs version specified in the package.json -> 0.0.0 wasn't available but 0.0.2 was
   > solution: update version specified in package form * to 0.0.2
