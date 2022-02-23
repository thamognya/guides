# librewolf-use-startpage
### This is a guide to make librewolf have a different start page for the homepage and new tabs.

<hr>

## Homepage

So to first to get the homepage as the needed startpage, go to settings > Home > New Windows and Tabs and set Homepage and new windows as `custom urls` and set it as your startpage website or local path to startpage. I recomend a website to make it easier so if you dont have a website, host it on gitlab or github.

<hr>

## Other tabs

For other tabs you need to go to librewolf's directory. Read this doc page <a href="https://librewolf.net/docs/settings/">Librewolf-Docs: settings</a> to find out the directory. For my case it is `/usr/lib/librewolf`. So go to `/usr/lib/librewolf` and then go to `defaults/pref` and make a file (you need root permissions) named <a href="https://raw.githubusercontent.com/ThamognyaKodi/librewolf-use-startpage/main/autoconfig.js"><code>autoconfig.js</code></a> with the following contents

`autoconfig.js`
```
pref("general.config.filename", "mozilla.cfg");
pref("general.config.obscure_value", 0);
pref("general.config.sandbox_enabled", false);
```

then go back to the original folder for me it is `/usr/lib/librewolf` and then make <a href="https://raw.githubusercontent.com/ThamognyaKodi/librewolf-use-startpage/main/mozilla.cfg"><code>mozilla.cfg</code></a> with the following contents:

`mozilla.cfg`
```
// Any comment. You must start the file with a single-line comment!
let { classes:Cc, interfaces:Ci, utils:Cu } = Components;

try {
  Cu.import("resource:///modules/AboutNewTab.jsm");
  let newTabURL = "PATH_TO_STARTPAGE_REPLACE_ME";
  AboutNewTab.newTabURL = newTabURL;
} catch(e) { Cu.reportError(e); }

// Auto focus new tab content
try {
  Cu.import("resource://gre/modules/Services.jsm");
  Cu.import("resource:///modules/BrowserWindowTracker.jsm");

  Services.obs.addObserver((event) => {
    window = BrowserWindowTracker.getTopWindow();
    window.gBrowser.selectedBrowser.focus();
  }, "browser-open-newtab-start");
} catch(e) { Cu.reportError(e); }
```

#### Note: replace "PATH_TO_STARTPAGE_REPLACE_ME" with your website or local path to startpage

save the file and restart librewolf and voila it should work.
