# Rails Commands

### Basic Commands
```sh
rails new <app_name> #=> Generate a new rails application
rails new <app_name> -T #=> Generate a new rails application without tests
rails new <app_name> -T --database=postgresql
rake assets:precompile
```
### Migrations
```sh
rails generate migration create_movies #=> Create migration create_movies
rake db:migrate #=> Apply migration
```

### Not classified
```sh
rake routes
rails console

# Install Postgres lib
sudo apt-get install libpq-dev

ADDING OR CHANGING MODEL ATTRIBUTES
$ rails g migration add_columnname_to_tablename columnname:datatype
follow this format to add a new attribute to a model
$ rails g migration rename_name_column_to_username
follow this format to rename an attribute in a model

DATABASE
$ rake db:reset
resets the DB
$ rake db:migrate
migrates the DB on development
$ heroku run rake db:migrate
migrates the DB on heroku
$ rake db:rollback STEP=2
removes the number of migrations you have specified
$ rake db:rollback VERSION=0
goes all the way back to the beginning

SCAFFOLDING
Generate a new scaffold w/options
$ rails g scaffold User name:string [attribute]:[type]

RPSEC
$ rails g integration_test [controllername] # generates a file in spec/requests
```
