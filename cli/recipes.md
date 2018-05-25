# Recipes

## Recipes

Maze generators can use a recipe to generate your application, and scaffold your application with controllers, models and views. Using a recipe you can get started with an maze application that extends or modifies the standard built in generator or provides additional features. For example you might want an API application that only renders JSON or use React or AngularJS for views.

### Maze New Command with a recipe

Add a recipe name command line argument to create a new maze application from the recipe.  
The recipe name that you use to generate the application is saved so that when you generate controllers, models and views with the scaffold generator the same recipe is used - you don't have to specify the recipe each time.

#### `maze new`

```text
maze new NAME OPTIONS

Arguments:
  NAME  name/path of project

Options:
  -d      Select the database database engine, can be one of: pg | mysql | sqlite (default: pg)
  --deps  Installs project dependencies, this is the equivalent of running (shards update)
  -t      Selects the template engine language, can be one of: slang | ecr (default: slang)
  -r      Use a named recipe.  See documentation at https://mazeframework.org.
```

### Example Usage

Using `maze new microsecond-blog -r damianham/mazebase` will generate a skeleton Maze application in `./microsecond-blog` using the _mazebase_ recipe that was provided by the github user _damianham_.

You can have a running web application in a matter of minutes:

1. `maze new microsecond-blog -r damianham/mazebase --deps`
2. `cd microsecond-blog`
3. `maze watch`

Now open a web browser for your new maze app at [http://localhost:3000](http://localhost:3000).

Full example in terminal:

```text
$ maze new microsecond-blog -r damianham/mazebase
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
Installing selenium (0.3.0)
$ maze watch
02:58:23 Watcher    | (INFO) Watching 22 files (server reload)...
02:58:23 Watcher    | (INFO) Building project App01...
02:58:31 Watcher    | (INFO) Terminating app App01...
02:58:31 Watcher    | (INFO) Starting App01...
02:58:31 NodeJS     | (INFO) Installing dependencies...
02:58:31 NodeJS     | (INFO) Watching public directory
02:58:31 Server     | (INFO) Maze 0.7.2 serving application "App01" at http://0.0.0.0:3000
02:58:31 Server     | (INFO) Server started in development.
02:58:31 Server     | (INFO) Startup Time 00:00:00.000182000
02:58:31 Watcher    | Watching 10 client files...
```

### Recipe sources

Maze can use a recipe from the following sources;

- The Maze framework recipe repository
- A github repository
- A local file system folder
- A URL

### Recipe repository

Visit the [recipe repository](https://github.com/mazeframework/recipes) to discover what recipes are available. The available recipes are listed in the [Contributions.md](https://github.com/mazeframework/recipes/blob/master/Contributions.md) file. Each recipe contributor provides additional information in their own Readme.

### Github repository

Specify a Github username and repository as the recipe source as in the example above.
E.g `maze new microsecond-blog -r damianham/mazebase` will generate a skeleton Maze application in `./microsecond-blog` from the github repository https://github.com/damianham/mazebase

### Local file system folder

Specify a local file system folder as the recipe source.  Use the absolute path to the recipe folder.
E.g. `maze new microsecond-blog -r /home/damian/recipes/myrecipe` will generate a skeleton Maze application in `./microsecond-blog` from the recipe located in the folder _/home/damian/recipes/myrecipe_.

### From a URL

Specify a URL to a zip file as the recipe source.  The zip file must contain the standard conttents of a recipe.
E.g. `maze new microsecond-blog -r https://github.com/mazeframework/recipes/blob/master/dist/react/preact_redux.zip` will generate a skeleton Maze application in `./microsecond-blog` from the recipe located in the zip file at the URL https://github.com/mazeframework/recipes/blob/master/dist/react/preact_redux.zip.

### Maze Generate Command

The generators in maze are a great way to get an application up and running quickly. In addition, they help keep code consistent and following convention. See the **Generate** option of the **Command Line Tool** for details about the generate command.

Once an application is generated with a recipe, it will be used by future generate or scaffold commands to maintain consistency with the recipe. For example, an application generated with a "json-api" recipe will continue to generate controllers and views according to the "json-api" recipe.

### Custom Recipe

When a recipe doesn't quite suite your requirements, it's easy to modify. Recipes are application stubs written in [Liquid](https://github.com/TechMagister/liquid.cr).  
Modified recipes can be stored and sourced locally or contributed back to the community repository.

Download a recipe that you want to modify, extract it, and use the extracted recipe on the command line. For example:

1. `wget https://git.io/vpdcz # zip file`
2. `mkdir ~/mymodular`
3. `unzip -d ~/mymodular modular.zip`
4. `# modify the recipe in ~/mymodular some way`
5. `maze new microsecond-blog -r ~/mymodular`
6. `cd microsecond-blog`
7. `shards install`
8. `maze watch`

Now open a web browser at [http://localhost:3000](http://localhost:3000).

It is important to give the absolute path to the recipe folder as the recipe command line argument to ensure that the recipe can be found when generating subsequent artifacts.

### Custom Repository

You can specify the location of a recipe repository in the `.maze.yml` file so that you can use recipes from an independent source. Add the **recipe\_source** item to the '.maze.yml' file with the URL of the website or website folder that contains the recipe zip files to use the recipes from the given URL. E.g

```text
type: app
database: sqlite
language: slang
model: granite
recipe: myrecipe
recipe_source: http://my.example.org/recipes
```

The scaffold generator would then use a recipe located at `http://my.example.org/recipes/myrecipe.zip`

### Clear Recipe Cache

If you set a recipe source URL you should also change the name of the recipe and/or you should clear the recipe cache otherwise a recipe with the same name in the recipe cache will be used rather than a recipe from the given recipe source.

The recipe cache is located in the current working directory and is created any time you specify a recipe name that is downloaded from the repository. Since you would usually specify a recipe when creating a new application the recipe cache will be located in the parent folder of the new application in a folder called `.maze_recipe_cache`.
