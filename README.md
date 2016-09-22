# Glimpse Preview

Thanks for checking out the Glimpse preview! By downloading this software, you agree to the license agreement.

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

Once setup, next time you run your application, Glimpse will inject a small widget (HUD - the Heads-Up-Display) into the bottom right hand corner of your page. HUD is intended to give you a 10,000ft view of your application and give you ongoing feedback around its workign. From here, you can click on the Glimpse logo to view full Glimpse Client. 

Alternatively, the Glimpse Client can be accessed (when the application is running, assuming on port 3000) at - http://localhost:3000/glimpse/client. If you access this resource directly, when prompted for the metadata endpoint, just accept the default.

## Package & Version Support

Glimpse for Node currently supports the following:
- Node Version 4.0 to 6.6.
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
