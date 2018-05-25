# CLI

Maze has a built in CLI tool, to make your life easier while developing applications.

Here is a list of the available commands:

* **d, deploy**     - Provisions server and deploys project.
* **db, database**  - Performs database maintenance tasks
* **e, encrypt**    - Encrypts environment YAML file. \[env \| -e --editor \| --noedit\]
* **x, exec**       - Executes Crystal code within the application scope
* **g, generate**   - Generate Maze classes
* **n, new**        - Generates a new Maze project
* **routes**        - Prints all defined application routes
* **w, watch**      - Starts maze development server and rebuilds on file changes

Read a long this guide to learn more about these command and how much time and efficient it can make your development experience.

## Getting Command Help

You can get help from each command by running `-h` or `--help` next to the command

Eg.

```text
$ maze --help
```

This will output to your shell the following documentation.

```text
maze [OPTIONS] SUBCOMMAND

Maze - Command Line Interface

  The `maze new` command creates a new Maze application with a default
  directory structure and configuration at the path you specify.

  You can specify extra command-line arguments to be used every time
  `maze new` runs in the .maze.yml configuration file in your project
  root directory

  Note that the arguments specified in the .maze.yml file does not affect the
  defaults values shown above in this help message.

  Usage:
  maze new [app_name] -d [pg | mysql | sqlite] -t [slang | ecr] -m [granite, crecto] --deps

Subcommands:
  d, deploy     # Provisions server and deploys project.
  db, database  # Performs database maintenance tasks
  e, encrypt    # Encrypts environment YAML file. [env | -e --editor | --noedit]
  x, exec       # Executes Crystal code within the application scope
  g, generate   # Generate Maze classes
  n, new        # Generates a new Maze project
  routes        # Prints all defined application routes
  w, watch      # Starts maze development server and rebuilds on file changes

Options:
  -d, --database  # Preconfigure for selected database. Options: pg | mysql | sqlite (default: pg)
  -m, --model     # Preconfigure for selected model. Options: granite | crecto (default: granite)
  -t, --template  # Preconfigure for selected template engine. Options: slang | ecr (default: slang)
  -h, --help      # Describe available commands and usages
  -v, --version   # Prints Maze version

Example:
  maze new ~/Code/Projects/weblog
  This generates a skeletal Maze installation in ~/Code/Projects/weblog.
```

## Usage

```bash
maze new [your_app] -d [pg | mysql | sqlite] -t [slang | ecr] --deps
cd [your_app]
```

### Options

* `-d` defaults to pg
* `-t` defaults to slang
* `--deps` will run `crystal deps` for you.

