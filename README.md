# Glimpse Preview

## Install Instructions

The easiest way to install Glimpse within an application is to configure NPM to use our private feed for @glimpse-scoped packages:

```
npm config set @glimpse:registry=https://www.myget.org/F/g-beta/npm/
```

Then, you can install glimpse:

```
npm install @glimpse/glimpse-node-agent --save
npm install @glimpse/glimpse-node-server --save
```

Next up is the initialization of Glimpse in your application. Make sure Glimpse is initialized before any other packages are imported/required.

```javascript
var glimpseAgent = require('@glimpse/glimpse-node-agent'),
    glimpseServer = require('@glimpse/glimpse-node-server')

    glimpseServer.server.init()
    glimpseAgent.agent.init({
        server: glimpseServer.server
    })
```

The Glimpse client can be accessed (when the application is running, assuming on port 3000) at: http://localhost:3000/glimpse/client

When prompted for the metadata endpoint, just accept the default.
