# RVM Commands

### Basic Commands
```shell
rvm current #=> Show current ruby version
rvm gemdir #=> list the full directory path for the current gemset

rvm install 1.9.3 #=> Install ruby version 1.9.3
rvm rubygems current #=> install the most recent RubyGems that RVM knows about

rvm use 2.1.2 #=> Use ruby version 2.1.2
rvm gemset create <gemset_name> #=> Create a new gemset
rvm use 2.1.2@<gemset_name> #=> Use ruby version 2.1.2 with the gemset specified.
rvm gemset use teddy #=> Use the gemset named teddy

rvm gemset list #=> list all named gemsets for the current ruby interpreter
rvm gemset list_all #=> list all named gemsets for all interpreters
rvm gemset empty <gemset_name> #=> removes all gems installed in the gemset
rvm gemset delete teddy #=> Delete the gemset named teddy
```