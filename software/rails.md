# Rails Commands

### Basic Commands
```sh
rails new <app_name> #=> Generate a new rails application
rails new <app_name> -T #=> Generate a new rails application without tests
rails new <app_name> -T --database=postgresql
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
```
