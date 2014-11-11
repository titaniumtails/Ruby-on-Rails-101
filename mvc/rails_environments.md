# Rails Environments

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
