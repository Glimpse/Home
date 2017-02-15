# Glimpse Preview

Thanks for checking out the Glimpse preview! By downloading this software, you agree to the license agreement.

## Latest News

- Feb 7, 2017 - Turn up the signal with 0.17.5. Read all about it in our [annoucement post](https://github.com/Glimpse/Home/issues/86).
- Jan 6, 2017 - Happy New Year, we've released 0.16.4!  Find out more in our [announcement post](https://github.com/Glimpse/Home/issues/85).
- Nov 22, 2016 - We've released 0.15.2, a minor update to last week's release. See our [annoucement post](https://github.com/Glimpse/Home/issues/82) for more info.
- Nov 17, 2016 - We've released version 0.14.1! This is the biggest release of Glimpse for Node yet. Find out more in our [annoucement issue](https://github.com/Glimpse/Home/issues/75).

---

## Node.js Installation Instructions

Glimpse releases are available via our custom NPM feed: [https://www.myget.org/F/g-beta/npm/](https://www.myget.org/F/g-beta/npm/)

Install the Glimpse agent and server packages by configuring NPM to use the feed (only) for @glimpse-scoped packages:

```bash 
> npm config set @glimpse:registry=https://www.myget.org/F/g-beta/npm/
```
 
That allows you to install Glimpse packages without specifying the registry:
 
```bash
> npm install @glimpse/glimpse-node --save
```

### Cloud Hosting 

If your Node.js application is hosted in the Cloud, create a `.npmrc` file to store the NPM feed in the root project folder.

`.npmrc`:

```text
@glimpse:registry=https://www.myget.org/F/g-beta/npm/
```

Then you can add `@glimpse/glimpse-node` as a project dependency in `package.json` and they will be installed as part of `npm install`. 

If your Node.js application is hosted in Azure, the Client will not be able to receive new requests from the application unless you set `responseBufferLimit` to `0` in the application's web.config, as shown in the example below.

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
     This configuration file is required if iisnode is used to run node processes behind
     IIS or IIS Express.  For more information, visit:

     https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
-->

<configuration>
  <system.webServer>
    <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
    <webSocket enabled="false" />
    <handlers>
      <!-- Indicates that the server.js file is a node.js site to be handled by the iisnode module -->
      <add name="iisnode" path="bin/www" verb="*" modules="iisnode" responseBufferLimit="0"/>
    </handlers>
    <rewrite>
      <rules>
        <!-- Do not interfere with requests for node-inspector debugging -->
        <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
          <match url="^bin/www\/debug[\/]?" />
        </rule>

        <!-- First we consider whether the incoming URL matches a physical file in the /public folder -->
        <rule name="StaticContent">
          <action type="Rewrite" url="public{REQUEST_URI}"/>
        </rule>

        <!-- All other URLs are mapped to the node.js site entry point -->
        <rule name="DynamicContent">
          <conditions>
            <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
          </conditions>
          <action type="Rewrite" url="bin/www"/>
        </rule>
      </rules>
    </rewrite>
    
    <!-- 'bin' directory has no special meaning in node.js and apps can be placed in it -->
    <security>
      <requestFiltering>
        <hiddenSegments>
          <remove segment="bin"/>
        </hiddenSegments>
      </requestFiltering>
    </security>

    <!-- Make sure error responses are left untouched -->
    <httpErrors existingResponse="PassThrough" />

    <!--
      You can control how Node is hosted within IIS using the following options:
        * watchedFiles: semi-colon separated list of files that will be watched for changes to restart the server
        * node_env: will be propagated to node as NODE_ENV environment variable
        * debuggingEnabled - controls whether the built-in debugger is enabled

      See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
    -->
    <!--<iisnode watchedFiles="web.config;*.js"/>-->
  </system.webServer>
</configuration>
```

## Node.js Configuration Instructions

Make sure Glimpse is initialized **before** any other `require()` or application logic.  (Glimpse will actually detect and warn you in that case.)

```javascript 
var glimpse = require('@glimpse/glimpse-node');

glimpse.init();
```

> If you use ES6 `import` via a trans-piler such as Babel, understand that it can reorder the generated `require()` statements. In that case, initialize Glimpse via an alternative application entrypoint as shown below.

### Sample Configuration

`app.js`:

```javascript
/*
 * Existing application logic.
 */
```

`glimpse.js`:

```javascript 
var glimpse = require('@glimpse/glimpse-node');

glimpse.init();

require('./app');
```

You can then run your application with Glimpse using the new entrypoint:

```bash
> node ./glimpse.js
```

Once setup, next time you run your application, Glimpse will inject a small widget (HUD - the Heads-Up-Display) into the bottom right hand corner of your page. HUD is intended to give you a 10,000ft view of your application and give you ongoing feedback around its working. From here, you can click on the Glimpse logo to view full Glimpse Client. 

Alternatively, the Glimpse Client can be accessed (when the application is running, assuming on port 3000) at - http://localhost:3000/glimpse/client. If you access this resource directly, when prompted for the metadata endpoint, just accept the default.

### Adding Script Tag for Static HTML Content

If you have static HTML content, you can enable Glimpse on your HTML page by adding the following script tag:
```
    <head>
        <script src="/glimpse/hud/main.js?hash={hash}" 
            id="__glimpse_hud" 
            data-client-template="/glimpse/client/?baseUrl=/glimpse/client&hash={hash}{&requestId,follow,metadataUri}" 
            data-context-template="/glimpse/context/?contextId={contextId}{&types}" 
            data-metadata-template="/glimpse/metadata/?hash={hash}">
        </script>

        <script src="/glimpse/agent/agent.js?hash={hash}"
            id="__glimpse_browser_agent"
            data-message-ingress-template="/glimpse/message-ingress/">
        </script>
    </head>
```

## Package & Version Support

Glimpse for Node currently supports the following:
- Node Version 4.0 to 7.5.
- [MongoDb Driver](https://www.npmjs.com/package/mongodb) Version 2.0.14 to 2.2.x.
- [Express.js](https://www.npmjs.com/package/express) Version 4.0 to 4.14.
- The native `http` module.
- The native `console` module.

For further support targets, please open an issue with your requested module and version.

## Issue Reporting

If you run into any problems, please open a new issue in this repo. A member of the team will follow up with you ASAP.


## Known Issues

 - You may see the console warning `Glimpse (1003): The package '@glimpse/glimpse-node-common' was imported before Glimpse was initialized.  Glimpse may not capture data related to that package.`  This warning can be ignored.

---

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
