# error-list
Errors and messages seen in console, and their solutions


## Kendo Grid

- cannot toggle group collapse/expand

   > I was using the kendo directive and trying to initialise with jquery
   > class name interefed
   
- update requests after incell changes were trying to update with the old value, not the new changed value.

   > the saveChanges() method on grid cannot be called within the save event function, i think it triggers before the actual dataitem is        updated, even if it is changed in cell.
   
## webpack-dev-server/keycloak (?) issues 

- 413 Request Entity Too Large
   
   > change entry from keycloak to demo
   ```var entry = DIST ? './standalone/viz.ui.builder.js' :'./demo/key-cloak.bootstrap.js';```
   TO
   ```var entry = DIST ? './standalone/viz.ui.builder.js' :'./demo/demo.js';```
   
   
## Webpack build

- outputs a zillion files i.e. images files

   > check externals prop includes all third party libs.

-  path is not a string. 
   This was a webpack error but did not break build
   Same msg was output to the build index.html
   
   > upgraded to:
   ```
         "html-webpack-plugin": "2.16.0"
   ```

- Long builds

   > use    
   ```
   "css-loader": "0.14.5",
   "postcss-discard-duplicates": "2.0.2"
   ```
   
   
- `WARNING in viz.ui.tags.min.js from UglifyJs
   Dropping unused function ...`
   
   > havent added 3rd part library that is being imported to the `external` property in my webpack.dist file
   
## Karma / Webpack

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

- `
   PhantomJS 2.1.1 (Windows 7 0.0.0) ERROR
     ReferenceError: Can't find variable: require
     at C:/Users/collsl/LaurenProjects/Storm/viz-ui-select/tests.webpack.js:5
   `
   
   > karma/webpack deps werent installed


## Angular

- Could'nt pass a value to a directive with $scope
   
   > the variable name was camelCase so the variable name in the view where the directive was being used needed to have '-'s
      e.g.
      ``` return {
        scope: {
            datasetMetas: '=',
            settings: '=',
            datasets: '='
        },
        ...```
       
       ```< my-directive settings=vm.settings dataset-metas= ...```
        

- view template not rendering
   
   > check component or directive name matches the normalised html el name (ie uiSelect -> `<ui-select></ui-select>` 
   
## Angular / webpack

- ` [HMR] Cannot apply update. Need to do a full reload! `


- ` bootstrap a40e730…:25 GET http://localhost:8080/a40e7300d99baba23b78.hot-update.json 404 (Not Found) `



- ` angular.js:13642Error: [$compile:tpload] Failed to load template:  `

    > forgot to change `templateUrl` to `template` in the directive

- `   Uncaught Error: [$injector:modulerr] Failed to instantiate module demoApp due to:
      Error: [$injector:modulerr] Failed to instantiate module {} due to:
      Error: [ng:areq] Argument 'module' is not a function, got Object 
   `
  > demo module was not exported for the keycloak config
  
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

      > ` .config()` and/or `.run()` were named
       ie `config('appAppConfig', appAppConfig)` 
       
      They expect a single argument only, function or array, and shouldn't be named


## NPM / Node
- ` (node) warning: possible EventEmitter memory leak detected. 11 listeners added. Use emitter.setMaxListeners() to increase limit. `
   > needed to destroy listeners ie 
      ```
          $scope.$on('$destroy', () => {
              vizServicesObserverService.removeListener('FORM_SETTINGS_RECALCULATED:' + exVm.formId, recalcVm);
          });

      ```


- `/c/Users/collsl/AppData/Roaming/npm/log-error: line 1: /node_modules/log-error/app/index.js: No such file or directory` error after trying to npm install -g a node script
   > needed to have `#!/usr/bin/env node` at the top of my script
   > see `http://stackoverflow.com/questions/33509816/what-exactly-does-usr-bin-env-node-do-at-the-beginning-of-node-files`


- `npm ERR! code 1 ` on `npm install` , no error message

   > deleting scoped packages and reinstalling seems to sometimes fix this error

- `
   npm ERR! Windows_NT 6.1.7601
   npm ERR! argv "C:\\Program Files\\nodejs\\node.exe" "C:\\Program Files\\nodejs\\node_modules\\npm\\bin\\npm-cli.js" "install" "--verbose"
   npm ERR! node v5.10.0
   npm ERR! npm  v3.8.3
   npm ERR! code EREADFILE
   `
   `
   npm ERR! Error extracting C:\Users\collsl\AppData\Roaming\npm-cache\fs\0.0.0\package.tgz archive: ENOENT: no such file or directory, open 'C:\Users\collsl\AppData\Roaming\npm-cache\fs\0.0.0\package.tgz'
   `
   
   > Problem with fs version specified in the package.json -> 0.0.0 wasn't available but 0.0.2 was
   
   > solution: update version specified in package form * to 0.0.2
   
   
## Other

