# Heroku

If you haven't done so please read the guides to install the [Maze CLI](https://github.com/mazeframework/docs/tree/5444592f267091cce244d8f7436cb56454605510/getting-started/installation/heroku.md)

## The Maze Heroku Buildpack

{% hint style="info" %}
Based on [Crystal Heroku Buildpack](https://github.com/crystal-lang/heroku-buildpack-crystal)
{% endhint %}

You can create an app in Heroku with Maze buildpack by running the following command:

```bash
$ heroku create myapp --buildpack https://github.com/mazeframework/heroku-buildpack-maze.git
```

The default behaviour is to use the [latest crystal release](https://github.com/crystal-lang/crystal/releases/latest). If you need to use a specific version create a `.crystal-version` file in your application root directory with the version that should be used \(e.g. `0.23.1`\).

## Requirements

In order for the buildpack to work properly you should have a `shard.yml` file,as it is how it will detect that your app is a Crystal app. Your application has to listen on a port defined by Heroku.

{% hint style="warning" %}
In Maze versions less than or equal to 0.3.7 add the following code to your `config/application.cr` file
{% endhint %}

```ruby
Maze::Server.configure do |settings|
  settings.host = "0.0.0.0"
  settings.port = ENV["PORT"].to_i if ENV["PORT"]?
end
```

To be able to decrypt and use production environment you'll need to set `ENV["MAZE_ENCRYPTION_KEY"]` to the value of your local projects `.encryption_key` file.

{% hint style="danger" %}
Never add `.encryption_key` to github. Maze adds it by default to your `.gitignore` file.
{% endhint %}

All that's left is to create a git repository, add the Heroku remote and push it there.

```text
$ git init
$ heroku git:remote -a [app-name]
$ git add -A
$ git commit -m "My first Maze app"
$ git push heroku master
```

## Using the Maze CLI on Heroku

When you deploy your project to heroku the maze build-pack will make available the `maze cli` to you via the `bin/maze` path.

To run an maze command just on heroku do the following:

```text
heroku run bin/maze [command]
```

{% hint style="info" %}
Read more about `heroku run` command on [Heroku Dev Center](https://devcenter.heroku.com/articles/one-off-dynos)
{% endhint %}

## The Heroku Procfile

To deploy your app to heroku you're going to need a `Procfile`. Create a Procfile at the root of your Maze application and add the following:

```yaml
release: bin/maze db migrate
web: bin/{your-app-name}
```

The Maze buildpack takes care of compiling the project for you but if you wish to run your project locally using the heroku command `heroku local` you must do the following steps.

Create an `.env` at the root of your Maze project and add the following 2 lines to the `.env`

```text
MAZE_ENV=development
PORT=3000
```

Then you must compile your project locally with the following command:

`crystal build src/{your-app-name}.cr -o bin/{your-app-name}`.

When the compilation process is complete a `bin/{your-app-name}` directory is added, with this binary of your application with this binary file ready you can proceed to run your application locally with heroku.

```text
heroku local
```

And should output something similar to:

```text
[OKAY] Loaded ENV .env File as KEY=VALUE Format
02:58:31 web.1   | 02:58:31 Server     | (INFO) Maze 0.7.2 serving application "heroku-app" at http://0.0.0.0:3000
02:58:31 web.1   | 02:58:31 Server     | (INFO) Server started in production.
02:58:31 web.1   | 02:58:31 Server     | (INFO) Startup Time 00:00:00.000182000
```

You're are now all set and ready to deploy with Heroku.

