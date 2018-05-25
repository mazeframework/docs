# Create New App

Before we begin, please take a minute to read the [Installation Guide](installation.md). By installing any necessary dependencies beforehand, we’ll be able to get our application up and running smoothly.

At this point, we should have Crystal and Maze installed. We should also have PostgreSQL and NodeJS installed to build a default application.

To verify you have Maze installed, run the command `maze -v` in your terminal window:

```bash
$ maze -v
Maze CLI (mazeframework.org) - vX.Y.Z
```

## Bootstrap an Application

To bootstrap your Maze application, run `maze new` with an absolute or relative directory path to the application directory it should create. Assuming that the name of your application is "weblog", let's run:

```bash
$ maze new weblog
```

Additionally, the following options may be passed to the above command:

* `-d` This specifies the database driver to use. It defaults to pg, for PostgreSQL.
* `-t` This specifies the template rendering engine. It defaults to slang, the Slim-inspired templating language.
* `--deps` This will download and install project dependencies for you, to save the additional step of having to type `shards install`.

Maze generates the [directory structure](https://github.com/mazeframework/online-docs/tree/77946b0fbe0e43bff1a43e42ac904d10ff436067/guides/getting-started/Installation/directory-structure.md#directory-structure) along with files necessary for the application.

Change your current directory to `weblog`, if that was the path you chose:

```bash
cd weblog
```

## Installing Dependencies

Now install project dependencies with `shards install`:

```bash
$ shards install
Using maze (0.7.2)
Using maze_router (0.0.3)
Using cli (0.7.0)
Using optarg (0.5.8)
Using callback (0.6.3)
Using string_inflection (0.2.1)
Using compiled_license (0.1.3)
...
Using jasper_helpers (0.2.0)
Using garnet_spec (0.1.1)
Using selenium (0.3.0)
```

## Creating the database

Maze makes it easy to interact with your database. Maze supports Postgres, MySql, and Sqlite.

Edit the database setting for your current environment by editing the file:

```text
{project_name}/config/environments/{current_environment}.yml
```

Maze looks at the `database_url` key for the default database connection string.

{% hint style="info" %}
Maze assumes that your PostgreSQL database will have a `postgres` user account with the correct permissions and no password set for this user. If that isn’t the case, update the `database_url` key with the correct database credentials for your environment.
{% endhint %}

With your database credentials ready, run the following command in your terminal window:

```bash
maze db create
```

This creates your application's Postgres database. It should output:

```bash
Created database weblog_development
```

And finally, we’ll start the Maze server:

```bash
maze watch
```

By default Maze accepts requests on port 3000. If we point our favorite web browser at [http://localhost:3000](http://localhost:3000), we should see the Maze Framework welcome page.

![Oh, yeah!](https://raw.githubusercontent.com/mazeframework/site-assets/master/images/maze-framework-welcome.png)

If your screen looks like the image above, congratulations!

You now have a working Maze application. If you don’t see the page above, try accessing it via [http://127.0.0.1:3000](http://127.0.0.1:3000).

Locally, the application is running in a Crystal process. To stop it, we hit ctrl-c once, just as we would terminate the program normally.

{% hint style="info" %}
The `maze watch` command watches for any changes in your source files, recompiling automatically. If you don't want this, you can compile and run manually:  
1. Build the app `shards build -v`  
2. Run with `./[your_app]`  
3. Visit [http://127.0.0.1:3000](http://127.0.0.1:3000)
{% endhint %}

