# Views (and Dynamic Content)

#####I. TEMPLATES
We could use HTML, but it is not dynamic or database driven. Instead, what we want is to be able to embed Ruby code into our templates. ERB or Embedded Ruby Code is a special language that allows us to put it into the HTML. To do this:
1) Correct file extension:
  E.g. hello.html.erb
  File is called "hello", processed by ERB, outputted as HTML.

2) Embed our code in the template,

Two things we use:
`<% code %>`  executes the code
`<%= code%>` outputs the code

#####II. VARIABLES
Views don't care where it comes from.  Everything is set up for it ahead of time, the controller sets everything up, the view just has to present it. To pass data from the controller to the view, we're going to use instance variables: @instance_variable. It is part of the object oriented programming in ruby and it says that this variable applies inside this instance of an object.

In our case, the controller is the object. **The controller is just a regular ruby class.** Rails creates an instance of that class and then we can have instance variables assigned inside of it. It is available in that action, and rendered to that view.

**NB** Before rails renders a template, it gathers together all the the controller's instance variables, and makes those available to the template. The way we transfer data from our controller to our view, is going to be exclusively through these instance variables.

ActionPack - because of this cozy relationship. But you can't go from view to get something from the controller. Controller sets everything up from the view.  The arrow from controller to view only goes one way.

#####III. LINKS

http://stackoverflow.com/questions/15012050/link-to-view-controller

We are going to use the `link_to` method. It looks like:
```ruby
link_to text, http://target.com/
```
Here there are two arguments. The link `text`, and the link `target`, or URL.

Or we can pass in a hash:
```ruby
link_to text.name, http://target.com/item.name
```

If you see from page source `link_to`  generates the same HTML.

#####IV. PARAMETERS
Key value pairs are part of params.
The ID however is special, and its going to come on the left side of the question mark. The page is after.
```ruby
http://localhost:3000/demo/hello/20?page=5
```

Parameters hash - HashWithIndifferentAccess.
params is a special method that returns a hash that contains all of the GET and POST variables in the request. Including all controller and actions.

Indifferent meaning that in this one case,
`params[:id]` and `params['id']` are the same.

When things come in through the URL parameter, it becomes a string. Parameters are always strings. If you need them to be integers or need to do math with them, you need to convert it using to_i. Ruby ERB tags will always convert it back to a string.

`<%= params.inspect %>` can make troubleshooting problems easier, it returns the full hash.
