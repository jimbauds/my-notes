# Cucumber

## To Classified
```sh
Rails 3
# add to end of Gemfile
group :test do
  gem 'cucumber-rails', :require => false
  gem 'cucumber-rails-training-wheels' # some pre-fabbed step definitions  
  gem 'database_cleaner' # to clear Cucumber's test database between runs
  gem 'capybara'         # lets Cucumber pretend to be a web browser
  gem 'launchy'          # a useful debugging aid for user stories
end

rails generate cucumber:install capybara
rails generate cucumber_rails_training_wheels:install
rake db:test:prepare
```
