---
slug: 13-view-the-storefront
id: hi3loykke6n7
type: challenge
title: Customize the code
teaser: A short description of the challenge.
notes:
- type: text
  contents: |-
    In the final challenge of the tutorial, you will see the online storefront for your coffee operation.

    It uses the Vue.js JavaScript framework to create a single-page web app (SPA).
    Teaching Vue.js is beyond the scope of this tutorial, but you get a flavor for how it was built, and see how the REST services you created in Part 2 are used by this app.
tabs:
- title: Terminal
  type: terminal
  hostname: vscode
- title: IRIS Coffee Company
  type: service
  hostname: vscode
  port: 4200
- title: VSCode
  type: service
  hostname: vscode
  path: /?folder=/opt/intersystems/src/frontend
  port: 8080
- title: IRIS
  type: service
  hostname: iris
  path: /csp/sys/UtilHome.csp?IRISUsername=_SYSTEM&IRISPassword=SYS
  port: 52773
difficulty: basic
timelimit: 300
---
The code has all been written for you, so let’s run it and see how it works.
First, let’s start installing some required packages.
That will take a few minutes, and we can make some edits those download.
In the VSCode’s terminal, enter the following commands.

```
yarn install
```

Now let’s run the app in a built-in development web server.

* Enter the following command:
```
yarn serve
```
* Switch to tab *IRIS Coffee Company*

You should see a list of products for sale.