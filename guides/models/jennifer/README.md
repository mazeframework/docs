# Jennifer

## What is Jennifer?

**Jennifer** is an ActiveRecord pattern for Crystal with great query DSL and migration mechanism.

{% hint style="info" %}
This section is based on [Jennifer's Docs](https://github.com/imdrasil/jennifer.cr/blob/master/docs/index.md). Also see [Maze Jennifer Example App](https://github.com/eliasjpr/maze-jennnifer-app-example).
{% endhint %}

## Installing Jennifer for Maze

### Generate a normal maze app

```text
maze new {project}
```

### Update your project shard.yml

Add this to your application's

```yaml
# Add the following dependencies
jennifer:
  github: imdrasil/jennifer.cr

sam:
  github: imdrasil/sam.cr
```

> Choose one of existing adapters for your db: [mysql](https://github.com/crystal-lang/crystal-mysql) or [postgres](https://github.com/will/crystal-pg).

Then in the console

```text
shards update
```

### Setup your database information

```yaml
defaults : &defaults
  host: localhost
  adapter: postgres
  user: root
  password: somepassword
  migration_files_path: db/migrations # this is the default location for all migrations

development:
  db: blog_development
  <<: *defaults

test:
  db: blog_test
  <<: *defaults
```

### Create a **jennifer.c**r under the **/config** directory

```ruby
require "colorize"

Jennifer::Config.read("config/database.yml", MAZE_ENV)

Jennifer::Config.configure do |conf|
  conf.logger = Logger.new(STDOUT)

  conf.logger.formatter = Logger::Formatter.new do |severity, datetime, progname, message, io|
    io << datetime.colorize(:cyan) << ": \n" << message.colorize(:light_magenta)
  end
  conf.logger.level = Logger::DEBUG
end
```

{% hint style="info" %}
Note that we pass the `MAZE_ENV` to `Jennifer::Config.read` this will allow Jennifer to use the correct database settings for the environment.
{% endhint %}

### Create a sam.cr in {project/src}

Jennifer uses Sam for running tasks pertinent to ORM operations. Sam is a Make-like utility which allows to specify tasks like Ruby's Rake do using plain Crystal. For how to use [Sam](https://github.com/imdrasil/sam.cr) visit the Github repository [https://github.com/imdrasil/sam.cr](https://github.com/imdrasil/sam.cr)

```ruby
# src/sam.cr
require "jennifer/adapter/postgres"
require "jennifer"

require "../config/jennifer"
require "../db/migrations/*"
require "sam"
require "jennifer/sam"
load_dependencies "jennifer"
Sam.help
```

### Edit your src/{project}.cr file

This should be done before you load your application configurations \(or at least models\). With Maze this is very easy. Also the order is very important the adapter should come before Jennifer.

```ruby
require "jennifer/adapter/postgres" # for postgres
require "jennifer"

require "maze"
require "./controllers/**"
require "./mailers/**"
require "./models/**"
require "./views/**"
require "../config/*"

Maze::Server.instance.run
```

You're all set with the configuration. Next using Jennifer Migrations and Models.

