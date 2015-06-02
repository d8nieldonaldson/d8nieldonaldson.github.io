---
layout: post
title: Getting Started with Cordova
---


http://blog.bitovi.com/getting-started-with-cordova-in-15-minutes-or-less/

step 3: i am running ohmy-zsh so instead of ~/.bash_profile I added export

```
ANDROID_HOME=/usr/local/opt/android-sdk
```
to ~/.zshrc, on a new line

then paste export

```
ANDROID_HOME=/usr/local/opt/android-sdk
```

to shell window using for project, or quit and reopen terminal




https://ccoenraets.github.io/cordova-tutorial/

module 1: Creating a Cordova Project
-------------------------------------
pretty straight forward, just need to have iOS and Android SDKs

Module 2: Building a Cordova Project
-------------------------------------
android takes foreverrrrrrrrrrr to build

Module 3: Setting Up the Workshop Files
---------------------------------------
nothing to report here

Module 4: Choosing a Data Storage Strategy
------------------------------------------
as stated, you don't access the app in your browser via localhost:5000, but instead by just opening the file wwww/index.html in your browser

Module 5: Using Native Notification
-----------------------------------
hey, we added a plugin!

Module 6: Avoiding the 300ms Click Delay
-----------------------------------------
make sure to add "FastClick.attach(document.body);" to the event handler you added in the previous module

Module 7: Setting Up a Single-Page Application
----------------------------------------------
add the renderHomeView() function to app.js after findByName()

in the Event Registration section, remove:

```js
$('.search-key').on('keyup', findByName);
$('.help-btn').on('click', function() {
    alert("Employee Directory v3.4");
});
```

Module 8: Using Handlebars Templates
-------------------------------------
both [handlebars](http://handlebarsjs.com/) and [ratchet](http://goratchet.com/) added to the project

when you are ready to test in iOS, just go to your terminal and run

```
cordova emulate ios
```

Module 9: Creating Views
-------------------------
HomeView.js should look like this:

```js
var HomeView = function (service) {

    var employeeListView;

    this.initialize = function () {
        // Define a div wrapper for the view (used to attach events)
        this.$el = $('<div/>');
        this.$el.on('keyup', '.search-key', this.findByName);
        employeeListView = new EmployeeListView();
        this.render();
    };

    this.render = function() {
        this.$el.html(this.template());
        $('.content', this.$el).html(employeeListView.$el);
        return this;
    };

    this.findByName = function() {
        service.findByName($('.search-key').val()).done(function(employees) {
            employeeListView.setEmployees(employees);
        });
    };

    this.initialize();

}
```

the other changes are to app.js, which should now look like:

```js
// We use an "Immediate Function" to initialize the application to avoid leaving anything behind in the global scope
(function () {

    /* ---------------------------------- Local Variables ---------------------------------- */
    HomeView.prototype.template = Handlebars.compile($("#home-tpl").html());
    EmployeeListView.prototype.template =
            Handlebars.compile($("#employee-list-tpl").html());
    var service = new EmployeeService();
    service.initialize().done(function () {
        $('body').html(new HomeView(service).render().$el);
    });

    /* --------------------------------- Event Registration -------------------------------- */
    document.addEventListener('deviceready', function () {
        StatusBar.overlaysWebView( false );
        StatusBar.backgroundColorByHexString('#ffffff');
        StatusBar.styleDefault();
        FastClick.attach(document.body);
            if (navigator.notification) { // Override default HTML alert with native dialog
                window.alert = function (message) {
                    navigator.notification.alert(
                        message,    // message
                        null,       // callback
                        "Workshop", // title
                        'OK'        // buttonName
              );
          };
      }
    }, false);



    /* ---------------------------------- Local Functions ---------------------------------- */


}());

```


Module 10: Implementing View Routing
------------------------------------

pretty much copy and paste, here is how your app.js should look:

```js
// We use an "Immediate Function" to initialize the application to avoid leaving anything behind in the global scope
(function () {

    /* ---------------------------------- Local Variables ---------------------------------- */
    HomeView.prototype.template = Handlebars.compile($("#home-tpl").html());
    EmployeeListView.prototype.template =
            Handlebars.compile($("#employee-list-tpl").html());
    EmployeeView.prototype.template = Handlebars.compile($("#employee-tpl").html());
    var service = new EmployeeService();
    service.initialize().done(function () {
        router.addRoute('', function() {
          $('body').html(new HomeView(service).render().$el);
        });
    router.addRoute('employees/:id', function(id) {
        service.findById(parseInt(id)).done(function(employee) {
            $('body').html(new EmployeeView(employee).render().$el);
        });
    });

      router.start();
    });

    /* --------------------------------- Event Registration -------------------------------- */
    document.addEventListener('deviceready', function () {
        StatusBar.overlaysWebView( false );
        StatusBar.backgroundColorByHexString('#ffffff');
        StatusBar.styleDefault();
        FastClick.attach(document.body);
            if (navigator.notification) { // Override default HTML alert with native dialog
                window.alert = function (message) {
                    navigator.notification.alert(
                        message,    // message
                        null,       // callback
                        "Workshop", // title
                        'OK'        // buttonName
              );
          };
      }
    }, false);



    /* ---------------------------------- Local Functions ---------------------------------- */


}());
```

Module 11: Using Hardware Acceleration
--------------------------------------

Just follow along, again :)

In step 2, it says to replace $('body').html() with slider.slidePage() in the routes section of app.js. That part of the file should look like this:

```js
service.initialize().done(function () {
        router.addRoute('', function() {
         slider.slidePage(new HomeView(service).render().$el);
        });
    router.addRoute('employees/:id', function(id) {
        service.findById(parseInt(id)).done(function(employee) {
           slider.slidePage(new EmployeeView(employee).render().$el);
        });
    });
```

Module 12: Using the Location API
---------------------------------

For step 1, go to your terminal window and enter:
```
cordova plugin add org.apache.cordova.geolocation
```

Step 2: just add a new li item to the ul in the #employee-tpl script, doesn't matter where






