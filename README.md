# nativescript-dev-tnscorepatcher
### NativeScript  TNS Core Patcher  (**TCP**)

## Purpose

This plugin allows you to include it as a dependancy of your own plugin; this plugin will during the build process automatically check all plugins to see if there is a file called: `plugin.tcp`  this file will tell TCP how to modify the tns-core-modules source to add any missing functionality to the TNS core modules; that your plugin needs.  

For example; lets take a plugin that needs to modify a delegate that currently TNS does not export.  You would create a `plugin.tcp` inside this file you would add something like:

```
exports.patch = function(PatchEngine) {
  vat patch = new PatchEngine('ui/web-view/web-view.ios.js');
  if (!patch.hasCode('exports.UIWebViewDelegateImpl = UIWebViewDelegateImpl;');
    patch.append(['// Needed for Nathanael's awesome plugin', 
                  'exports.UIWebViewDelegateImpl = UIWebViewDelegateImpl;']);
    patch.apply();
  } 
};
```

Simply put this is the simplest type of patch, you can pass and array of string to append to the bottom of the file; if it doesn't already exist.

The second type of patch, is you can also create a diff patch, which is a bit more complex to setup.

If you are interested in helping make this project a reality I am discussing issues and ideas in the issue tracker..
  
