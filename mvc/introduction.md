# MVC
The object-oriented approach to design. Separation of concerns - Instead of one block of code, that handles business logic, presentation to the user.

[**Models**](#model) - many things are objects in our models. Most comment will be our data.

_(Handles Data)_
_(Rails library name: ActiveRecord)_

[**View**](#views) - Is the presentation layer. It's what the user sees and interacts with. HTML CSS Javascript.

_(Handles Presentation)_
_(Rails library name: ActionView -> ActionPack)_

[**Controller**](#controller) - processes and responds to user requests on the view, such as clicking links and submitting forms. The controller will make a decision based on the request and controls what happens in response. It controls the interaction between our models & views. Controller is more general, secretary, in the broad range of MVC.

_(Handles Decisions)_
_(Rails library name: ActionController -> ActionPack)_


![MVC](https://www.dropbox.com/s/s21gkbekh9o2tur/MVC%20overview.tiff "MVC Overview")

![MVC Library names](https://dl.dropboxusercontent.com/u/45502976/MD%20Images/MVC%20rails%20lib%20names.tiff "MVC Libary names")

The Model - database portion is optional, but the MVC is essential, the minimum amount that a Rails application needs.

-----------


---------

##Server Request-Response handling

Whereas `http-server` gives you the requested files (e.g. the local files, it gets the specific files and folders). It's dumb. Everything is visible via the public folder.  First, the web server will look inside the projects public directory, for any file whose path name exactly match the request that came in. If it finds that file, we will return that file to the browser, and never access the rails framework. That makes sense. There's no reason to use the framework when the request is for a self contained, static HTML page or image. And it really speeds things up when the server is gathering images, style sheets, or other static assets to send back to the browser. It makes page loads as quick as possible. It will satisfy the request within the public directory before it goes to the rails framework. Image assets also can be placed here so it doesn't have to bother the Rails framework, and be loaded quickly as possible.

But, whenever the web server doesn't find the matching file, next, it ask the Rails Framework to handle the request. The request goes to Rails **routing**.  Its about Routes. Routing parses the url to determine which controller and action to use. It will then execute the controller action. Make request to the Model as needed and then finally render our View, just like we saw with the MVC architecture.


![MVC Rails in Detail](https://www.dropbox.com/s/igh8ow0ejl93vu1/MVC%20Rails%20in%20detail.tiff "MVC Rails in detail")


**Setting up**

1) A routes file. So we know what files to get. (rails.rb)

2) Set-up a controller: Create a welcome controller, that inherits the Application controller.

3) Then creates a views file (HTML). Index is the name of the action, on that controller.

Rails does a lot of stuff, by convention.


##Router

There are 3 kinds of routes:
+ simple route
+ default route
+ root route

#####Simple route

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

#####Default route
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

#####Root route
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

-------

##Views (and Dynamic Content)

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

-----

##Databases
We usually create a model without a database first, and then add in the database connectivity later. But most models an rails will be connected to database tables; and in real world development, the process of creating those models, usually begins by first defining the database tables.

A database table is similar to an Excel table with columns and rows:
![Database Table Spreadsheet](https://www.dropbox.com/s/j8q8l2u35aoeyr8/Database%20tables.tiff "Database Table")
But they are not laid out in front of us like a visual medium above. We have to issue commands to interact the database.

You can have multiple tables. And so, databases can also have relationships between tables. This is why we call them: **Relational Databases**.


####Vocabulary
+ **Database** - a set of tables
  + not the same thing as  "a table". Its is a collection of tables.
  + One database = one application (typically).
  + Usually in snake_case
  + Access permissions are granted at database level

+ **Table**
  + A set of columns and rows
  + 1 Table = 1 Model
  + Plural
  + Where relationships are defined
+ **Columns** - These are table fields that define the data that will be stored. For e.g. `first_name` or '`city`.

+ **Column** -  A set of a single simple type, like a string or integer. (In a Rails Model, this is a single attribute).

+ **Rows**  - are the individual records or instances. For e.g. If I have 20 customers, I have 20 rows.

+ **Row** - Single record of data. E.g. "harry", "wong", "harrys@world.com"

+ **Field** - Intersection of a column and a row. E.g. Name: "Harry".

+ **Index** - Increases the lookup speed, like the back of a book.

+ **Foreign keys** - A table column, whose values reference rows in another table. Foreign keys plovide a relationship that is the foundation of relational databases. E.g. `post_id` Its singular.
**TIP**: Put indexes on foreign keys, so you can look up these ∝ very quickly

+ **Schema** - The structural definition of the database; the tables, the columns, the indexes, everything that makes up the database. If we import a schema into our database, it will create a complete database for us, although with no data in it, but with the correct structure.

+ **CRUD** - The 4 main ways we interact with the database.
  * Create  new data
  * Read    existing data
  * Update  existing data with new data
  * Delete  existing rows of data



###Rails Environments

We even have different databases for each environment, as seen in `database.yml`. Having a production database, a development database and a testing database is best practice.

It is possible to add additional environments. If you want to have a staging environment or a QA environment, something like that, but these are the 3 default environments that come with Rails:

#####Development
While we develop the application, where we might want all error details to be visible so that we can see them and fix them.

After release, we can still use the development database for developing the app.We can add data and delete data as we're testing and not worry that we're modifying the valuable production data.

For e.g, if our application is sending emails, then we might have one set of email configurations for development, and a different set for production.

#####Production
When you put your application on a live server, for the public to use. Don't want errors or details about our code exposed to the general public, we probably want to display a more general Something Went Wrong page instead.

#####Test
This environment contains code that tests our application code to make sure that it's doing what we expect. The tests themselves can add and delete records but without making changes to either our production data or our development data.

###Rake

* Is a ruby implementation of UNIX `make`.

* A key part of the way that rake works is by using the `Rakefile`, which is inside the root of our application. If you open that file, you'll see that it contains Ruby code to load up the basics of our application and then they'll load up the rake tasks that are built into Rails.

* `rake -T` lists all the tasks that `rake` can do. Most have `db` in front of them, meaning they are used for working with the database.

* We can pass environment variables to `rake`, if you have configure your `database.yml` with production or testing information.  The default environment is development.

###Migrations




==============


###Rails' Full Stack Relationship
![Full Stack Relationship](https://dl.dropboxusercontent.com/u/45502976/Markdown%20Images/Rails%20Relationship%20II.jpg "Full Stack Relationship")
