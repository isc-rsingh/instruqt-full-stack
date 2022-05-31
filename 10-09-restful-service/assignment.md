---
slug: 09-restful-service
id: nybykbczjwwh
type: challenge
title: Your first RESTful Service
teaser: Build RESTful Services
notes:
- type: text
  contents: |-
    Now that we have database tables represented as ObjectScript code, and we know how to query the database using SQL and ObjectScript, we’re ready to build Web APIs. We'll connect an ObjectScript class to the Web and create "routes" so that certain URLs trigger the execution of certain methods in the class.

    ![image](https://dev-start.intersystems.com/wp-content/uploads/2021/03/IrisCoffee-Sketch3-01-e1616128053104-1024x307.png)
tabs:
- title: IRIS
  type: service
  hostname: iris
  path: /csp/sys/sec/%25CSP.UI.Portal.Applications.WebList.zen?IRISUsername=_SYSTEM&IRISPassword=SYS
  port: 52773
- title: VSCode
  type: service
  hostname: vscode
  path: /?folder=/opt/intersystems/src/services
  port: 8080
difficulty: basic
timelimit: 500
---
<style>
.lightbox {
  display: none;
  position: fixed;
  justify-content: center;
  align-items: center;
  z-index: 999;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  padding: 1rem;
  background: rgba(0, 0, 0, 0.8);
}

.lightbox:target {
  display: flex;
}

.lightbox img {
  max-height: 100%
}
</style>
With the basic JSON support set up, we can build a service.
* Move the file `Handler.cls` from the `src_Sample/ICO` folder to `src/ICO`
* Right-click on the file and choose "Import and Compile"

Now that we’ve written the middleware REST APIs, the final step in making the services work is to expose them to the web.

InterSystems IRIS provides a tool to route web requests to ObjectScript code in much the same way as Node.js Express or Python Flask. Let’s use the Management Portal to hook this IRIS class into the web.

* Click on the "IRIS" tab
* Click the *Create New Web Application* button.
* Under *Name*, enter `/api/coffeeco` (the base endpoint).
* Under *Namespace*, select *USER*.
* Make sure *Enable Application* is checked.
* Under *Enable*, select *REST*.
* For the *Dispatch Class*, type `ICO.Handler` (the IRIS Class all URLs starting with `/api/coffeeco` will be dispatched to).
* Under *Security Settings*, check *Unauthenticated* and *Password* for *Allowed Authentication Methods*.
* Click *Save* next to the title Edit Web Application.

<a href="#editwebapp">
  <img alt="alt text" src="https://dev-start.intersystems.com/wp-content/uploads/2021/03/edit_web_app-1024x524.png" />
</a>

<a href="#" class="lightbox" id="editwebapp">
  <img alt="alt text" src="https://dev-start.intersystems.com/wp-content/uploads/2021/03/edit_web_app-1024x524.png" />
</a>

Now you will see new tabs, one of which is *Application Roles*.
Click that tab, then *%All* under the *Available* list, then click the right arrow to copy it to the *Selected* list. Click *Assign*.

<a href="#assignrole">
  <img alt="alt text" src="https://dev-start.intersystems.com/wp-content/uploads/2021/03/edit_web_app_assign-768x750.png" />
</a>

<a href="#" class="lightbox" id="edassignroleitwebapp">
  <img alt="alt text" src="https://dev-start.intersystems.com/wp-content/uploads/2021/03/edit_web_app_assign-768x750.png" />
</a>
