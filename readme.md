[![npm (@glimpse/glimpse)](https://img.shields.io/npm/v/@glimpse/glimpse.svg)](https://www.npmjs.com/package/@glimpse/glimpse)
[![#ProjectGlimpse](https://img.shields.io/badge/tweet-%23ProjectGlimpse-blue.svg)](https://twitter.com/intent/tweet?hashtags=projectGlimpse&tw_p=tweetbutton)

# Project Glimpse: Node Edition

[![Join the chat at https://gitter.im/GlimpseHome/Lobby](https://badges.gitter.im/GlimpseHome/Lobby.svg)](https://gitter.im/GlimpseHome/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Glimpse is an experimental **[npm package](https://www.npmjs.com/package/@glimpse/glimpse)** that gives you in-depth insights about the **client and server sides** of your **Node.js** apps. More **efficient debugging** means **faster development**. Best of all, it’s free.

![Project Glimpse: Node Edition Screenshot](http://node.getglimpse.com/img/front-page/hero1.7848ce21.svg)

Full details and documentation available at [http://node.getglimpse.com](http://node.getglimpse.com).

## [Latest news](https://github.com/glimpse/Home/issues?utf8=%E2%9C%93&q=is%3Aissue%20label%3AAnnouncement%20)

- Mar 21, 2017 - It's all about services in 0.18.9. Find the details in our [announcement post](https://github.com/Glimpse/Home/issues/93).
- Feb 7, 2017 - Turn up the signal with 0.17.5. Read all about it in our [announcement post](https://github.com/Glimpse/Home/issues/86).
- Jan 6, 2017 - Happy New Year, we've released 0.16.4!  Find out more in our [announcement post](https://github.com/Glimpse/Home/issues/85).
- Nov 22, 2016 - We've released 0.15.2, a minor update to last week's release. See our [announcement post](https://github.com/Glimpse/Home/issues/82) for more info.
- Nov 17, 2016 - We've released version 0.14.1! This is the biggest release of Glimpse for Node yet. Find out more in our [announcement issue](https://github.com/Glimpse/Home/issues/75).

---

## Getting started

  1.  In your app's root directory, use npm to install Glimpse.
  ```bash
  npm install @glimpse/glimpse --save-dev
  ```
  2. Initialize Glimpse before any other `require()` or application logic (typically at the top of index.js or app.js).
  ```javascript
  if (process.env.NODE_ENV !== 'production') {
    require('@glimpse/glimpse').init();
  }
  ```
  3. Open your app in a browser. The Glimpse HUD should now be at the bottom right of your app.

For more help, [check out the detailed steps and more ways to get started](http://node.getglimpse.com/docs/setup/getting-started/).

## Package & version support

Project Glimpse: Node Edition currently supports the following:
- Node.js version 4.0 to 7.10.
- [Express.js](https://www.npmjs.com/package/express) version 4.0 to 4.15.
- The native `http` module.
- The native `console` module.

For further support targets, please open an issue with your requested module and version.

## Issue reporting

If you run into any problems, please open a [new issue](https://github.com/aspnet/home/issues/new) in this repo. A member of the team will follow up with you ASAP.

---

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
