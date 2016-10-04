# error-list
Errors and messages seen in console, and their solutions


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
      ` in the webpack.make

