###Rake

* Is a ruby implementation of UNIX `make`.

* A key part of the way that rake works is by using the `Rakefile`, which is inside the root of our application. If you open that file, you'll see that it contains Ruby code to load up the basics of our application and then they'll load up the rake tasks that are built into Rails. 

* `rake -T` lists all the tasks that `rake` can do. Most have `db` in front of them, meaning they are used for working with the database.

* We can pass environment variables to `rake`, if you have configure your `database.yml` with production or testing information.  The default environment is development. 