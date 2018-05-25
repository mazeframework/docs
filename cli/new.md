# New

## `maze new`

This is the first command that you will run when generating a new Maze application. It creates a new Maze application with a default directory structure and configuration setting at the path you specify.

An `.maze.yml` configuration file is generated a long with the default application directory structure. This stores some metadata for the Maze CLI to make use of for generating migrations, scaffolding templates, and more.

```text
maze new OPTIONS NAME

Arguments:
  NAME  name/path of project

Options:
  -d      Select the database database engine, can be one of: pg | mysql | sqlite (default: pg)
  --deps  Installs project dependencies, this is the equivalent of running (shards update)
  -t      Selects the template engine language, can be one of: slang | ecr (default: slang)
  -r      Use a named recipe.  See documentation at https://mazeframework.org.
```

See the **Recipes** option of the **Command Line Tool** for information about using recipes to generate applications.

### Example Usage

Using `maze new microsecond-blog` will generate a skeleton Maze application in `./microsecond-blog`. You can have a running web application in a matter of minutes:

```text
maze new microsecond-blog -s sqlite --deps
cd microsecond-blog
maze watch
open http://localhost:3000
```

Full example in terminal:

```text
$ maze new microsecond-blog
Rendering App microsecond-blog in ./microsecond-blog
new       .maze.yml
new       .maze_secret_key
new       .gitignore
new       .travis.yml
new       config/application.cr
new       config/database.yml
... [clipped]
new       src/views/layouts/_nav.slang
new       src/views/layouts/application.slang
new       src/microsecond-blog.cr
$ cd microsecond-blog/
$ shards install
Updating https://github.com/mazeframework/maze.git
Updating https://github.com/luislavena/radix.git
... [clipped]
Installing garnet_spec (0.1.1)
$ maze watch        
02:58:23 Watcher    | (INFO) Watching 22 files (server reload)...
02:58:23 Watcher    | (INFO) Building project microsecond-blog...
02:58:31 Watcher    | (INFO) Terminating app microsecond-blog...
02:58:31 Watcher    | (INFO) Starting microsecond-blog...
02:58:31 Server     | (INFO) Maze 0.7.2 serving application "microsecond-blog" at http://0.0.0.0:3000
02:58:31 Server     | (INFO) Server started in development.
02:58:31 Server     | (INFO) Startup Time 00:00:00.000182000
02:58:31 Watcher    | Watching 10 client files...
```

