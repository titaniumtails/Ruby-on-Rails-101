# Controller

The Controller processes and responds to user requests on the view, such as clicking links and submitting forms. The controller will make a decision based on the request and controls what happens in response. It controls the interaction between our models & views. Controller is more general, secretary, in the broad range of MVC.

Inside controllers are usually defined methods like `index`, called actions. This is actually a simple method, but when it's in this context with the controller we often cal lit an action.

`params` are pre-defined

```
? variable = value
```

**Helper** is a module, where we have functions, that are available in the views. listed there can be propagated throughout. Is for a specific function to help.

Singular or Plural? A Model is singular because it references a single object like User. A controller is plural because it is the controls (methods) for the collection of Users. How one names the routes is all up to that individual developer.

Good practice to have an action for each template. If nothing else, it tell there developer  of a possible choice for a template.

```ruby
def index
  end

def hello
  end
```
Default behaviour - There must be a template for each of these actions.

Or I can specify a template:
```ruby
def index
render('demo/hello')
  end

def hello
  end
```
Or in more verbose:
```ruby
def index
render(:template => 'demo/hello')
  end
```
Both will now go to the hello page.

We can specify a re-direct:
```ruby
  def other_hello
  	redirect_to(:controller => 'demo', :action => 'index')
  end
```
In short form using the defaults  (that we are in the demo controller so it will automatically go to demo:
```ruby
def other_hello
   	redirect_to(:action => 'index')
  end

  def lynda
  	redirect_to('http://lynda.com')
  end
```
