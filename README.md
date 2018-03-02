#Local Nationbuilder Bootstrap Styling

## Overview

Nationbuilder theme development can be a pain, if you don't setup Dropbox syncing you need to upload various changes through the website, click save/publish, refresh in your browser and (hope) that those changes don't affect live users until you're ready.

A solution to this problem for the CSS is to include a script in your layout.html, at the bottom of the head section which will import styles that you are working on locally.

This repo includes the default Bootstrap custom theme downloaded from Nationbuilder, basic live-reloading, a development server and sass compilation, which can be used in conjunction with localStorage in your browser to enable independent local development of styles with immediate browser feedback and no .

## Quick Start Guide

###Nationbuilder Environment

Skip this if someone else has already has done this.

Otherwise, update theme.html to include either
```
<script type="text/javascript" src="http://localhost:8080/development-code.js"></script>
```
or for a version that you can run in production that check for a localStorage property before loading
```
<script type="text/javascript">
  if(typeof(localStorage !== 'undefined')){
    var devCodeUrl = localStorage.getItem("development-code-url");
    if(devCodeUrl){
    		var head = document.head;
    		var script = document.createElement("script");
   			script.type = "text/javascript";
        script.src = devCodeUrl;
    	  head.appendChild(script);
    }
  }
 </script>
```

###Local Development Environment

####Clone the repository
```
git clone https://github.com/smd80p/nb-theme-bootstrap-lp
cd nb-theme-bootstrap-lp
npm install # Local dependencies if you want to hack
```

####Start the dev server
```
npm run dev
```

####Navigate to your nationbuilder live site

If you're using the production localStorage option add a local storage key pointing to your local storage:

```
localStorage.setItem("development-code-url", "http://localhost:36291/development-code.js")
```

####Develop the theme style

Edit files under `src` and the browser should reflect your changes automatically

####Debugging

If the webpage doesn't automatically update, check whether the websocket connection to your local server succeeded in the console.

If local compilation is failing, check the errors in the local console.  If src includes the theme downloaded directly from Nationbuilder it's possible the compilcation may fail due to missing 'framework_countdown2', comment that dependency out to enable local compilation.


