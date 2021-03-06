# Linking Events Together

ColdBox provides you with a nice method for generating links between events by leveraging an object called `event` that is accessible in all of your layouts/views and event handlers.  This `event` object is called the request context object which models the incoming request and even contains all of your incoming `FORM` and `URL` variables in a structure called `rc`.

Edit the `views/virtual/hello.cfm` page and wrap the content in a `cfoutput` and create a link to the main ColdBox event, which by convention is `main.index`.

```
<cfoutput>
<h1>Hello from ColdBox Land!</h1>
<p><a href="#event.buildLink( "main.index" )"#>Go home</a></p></cfoutput>
```

This code will generate a link to the `main.index` event in a search engine safe manner and in SSL detection mode.  Go execute the event: `http://localhost:{port}/virtual/hello` and click on the generated URL, you will now be navigating to the default event `/main/index`.  This technique will also apply to FORM submissions:

```html
<form action="#event.buildLink( 'user.save' )#" method="post">
...
</form>
```


> **Tip** You can visit our API Docs for further information about the `event` object and the `buildLink` method: http://apidocs.ortussolutions.com/coldbox/current/index.html?coldbox/system/web/context/RequestContext.html. For extra credit try to use more of the `buildLink` arguments.

## URL Structure & Mappings

ColdBox allows you to manipulate the incoming URL so you can create robust URL strategies especially for RESTFul services.  This is all done by convention and you can configure it via the file `config/routes.cfm` for more granular control.  

We have now seen how to execute events via nice Search Engine Safe URLs.  Behind the scenes, ColdBox translates the URL into an executable event string just like if you were using a normal URL string:

* `/main/index` -> `?event=main.index`
* `/virtual/hello` -> `?event=virtual.hello`
* `/admin/users/list` -> `?event=admin.users.list`
* `/handler/action/name/value` -> `?event=handler.action&name=value`
* `/handler/action/name` -> `?event=handler.action&name=`


By convention, any name-value pairs detected after an event variable will be treated as an incoming `URL` variable. If there is no pair, then the value will be an empty string.

> **Tip** If using full URL rewrites via CommandBox or any other web server, open the `config/routes.cfm` and eliminate the `index.cfm` from the `setBaseURL()` calls. This will remove any `index.cfm` to be generated via `buildLink()` calls.

<br>

> **Tip** You can find much more information about layouts and views in our [full docs](/full/routing/index.md)





