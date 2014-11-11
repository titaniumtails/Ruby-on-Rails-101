# Routes

There are 3 kinds of routes:
+ simple route
+ default route
+ root route

##Simple route

Looks like:
```ruby
get "welcome/index"
```
Which is actually short form for:
```ruby
match "welcome/index",
  :to => "welcome#index",
  :via => :get
```

It is matching the string `"welcome/index"`, and sending to the controller and action `"welcome#index"`, via `get`. This matches an **exact** string. Then you would need a static string for every page! That's why we have the default route.

##Default route
A routing rule that can handle many cases, parse the string into many components.
The structure is like this. Always in that order:
```ruby
:controller/:action/:id
```
This is not considered a best practice anymore. But it is good to get a feel for how it works.

E.g.
```ruby
GET /students/edit/52  -->   Students Controller, edit action
```
**NB**. The default action is always index.


##Root route
When you go to the root of the application, and there is nothing to match, you tell it where to direct the request. this essentially becomes your homepage for the application. Root is already defined, there are defaults.
```ruby
root 'welcome#index'
```

`root 'welcome#index'` is the same as  `get '/' => 'welcome#index'`

As soon as you put something afterwards you need to put the fat arrow with its hash.
```ruby
welcome/show/:id => welcome#show
```
after the fat arrow, it means: welcome means its going into the welcome controller,

**NB** Routes are processed from top to bottom on this file.
