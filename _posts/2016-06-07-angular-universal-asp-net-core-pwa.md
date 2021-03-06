---
layout: post
title: Progressive Web App rendered with Angular Universal and ASP.NET Core
published: true
---

I’ve always wanted to start a project where I could render an angular 2 web app with ASP.NET Core. Now, thanks to Steve Sanderson, it’s very easy. 

Also I wanted to play a little bit with Progressive Web Apps, which will enable offline access, push notifications, home screen installation, etc and improve my angular 2 skills.

I have created this [github repo](https://github.com/manuelreina/angular2-aspnet5-crud) which contains all the code. This progressive web app is composed of 2 pages, the home page and a simple CRUD page.

**BUILT WITH**

 - Angular 2
 - ASP.NET Core
 - Angular Universal
 - Progressive Web Apps
 - Webpack
 - Grunt

You can see the demo [here](https://angularuniversal-vnext.azurewebsites.net/)

This post **summarizes** all the steps and the issues I had in order to put everything together.



**RESOURCES**

 - In order to create a template capable of rendering **angular 2 with ASP.NET Core**, follow [Steve Sanderson blog post]. Note: I am using the RC1 template version.
 - **[Progressive web apps]** (Service worker, manifest, push notifications, home screen installation, etc).
 - Angular 2:
	 - https://angular.io/docs/js/latest/quickstart.html
	 - If you have a pluralsight account, I recommend [John Papa's pluralsight course](https://app.pluralsight.com/library/courses/angular-2-first-look)
	 - http://blog.thoughtram.io/
	 - 

**ISSUES**

 1. 	I am using **Visual Studio 2015 update 2** and when I updated to Angular 2 RC I had an issue with the VS typescript compiler. It threw the error “map does not exist on observable response”. It wasn’t big problem because I am using webpack to compile typescript but anyway here it’s the [solution]. 
 2. **Azure**. I am newbie with Azure and I had a few issues to make this project work.

 -   Everything worked like a charm in IIS Express but when I published in Azure I got errors.
 - As I couldn’t get much info about the errors I published locally.
	 - I found out that the node dependencies weren’t installed.
	 - I installed them and then I had another error:  `Cannot find module './wwwroot/dist/vendor-  manifest.json'.`
	 - I open [this issue] and Andrei Tserakhau helped me to solve it.
 - I couldn’t get the project.json “scripts” section work when publishing in Azure, so I decided to install everything manually.
 - Make sure your azure instance has an NPM version 3+. 
	 -   Open the Kudu tool, under the tools menu.
	 - See available “Runtime versions”.
	 - Go back to your resource in Azure and change the app setting “WEBSITE_NODE_DEFAULT_VERSION” with the corresponding version. Note: I use 5.4.0

 - NPM install
	 - Use the KUDU tool again to open a “Debug console”. 
	 - Install webpack globally. NPM install webpack –g
	 - Now navigate to the src of your app. E.g. D:\home\site\src
	 - Install the rest of dependencies. NPM install.
 - Finally make sure you don't have duplicate global.json files. In my case I had one under the approot folder and the one of my project. Removing the project's global.json solved my problem, but again, I think it has to do with my project structure and I have to learn more about asp.net 5 and azure deployment.

Hope it helps!


[Steve Sanderson blog post]: <http://blog.stevensanderson.com/2016/05/02/angular2-react-knockout-apps-on-aspnet-core>
[Progressive web apps]: <https://developers.google.com/web/fundamentals/getting-started/your-first-progressive-web-app>
[solution]: <https://github.com/Microsoft/TypeScript/issues/8518>
[this issue]: <https://github.com/aspnet/JavaScriptServices/issues/104>
