# Maze Auth

**Prerequisites**

* Familiar with MVC and terms such as Migrations, Database
* Maze Framework CLI already installed \([Installation Instructions](../guides/installation.md)\)
* Terminal console

## Overview

Virtually all web applications require a registering and authenticating users. As a result, most web frameworks have an excessive amount of options for implementing authentication. Maze Framework differs by providing a built-in generator for simple yet secure authentication that is sufficient yet easily extended at a later time. Maze allows you to get started writing your application without getting bogged down in application boilerplate.

## Using Maze Auth Generator

### 1. Generate Blogsy App

First, we generate our app by typing the following command in a terminal console.

```bash
maze new blogsy --deps -d sqlite
```

{% hint style="info" %}
The `--deps` will automatically install project dependencies. `-d sqlite` builds the project with a SQLite database.
{% endhint %}

### 2. Go to your project directory

Commands are performed within the root directory of our project.

```bash
cd blogsy
```

### 3. Scaffold the User Authentication

Next, we will scaffold our authentication system. The scaffold will generate several files to build a basic authentication system.

```bash
maze g auth User
```

The above command will give you the following output:

```text
08:26:45 Generate    | Rendering Auth user
08:26:45 Generate    | new       config/initializers/granite.cr
08:26:45 Generate    | new       spec/models/user_spec.cr
08:26:45 Generate    | new       spec/models/spec_helper.cr
08:26:45 Generate    | new       spec/controllers/spec_helper.cr
08:26:45 Generate    | new       db/migrations/20180110202645523_create_user.sql
08:26:45 Generate    | new       db/seeds.cr
08:26:45 Generate    | new       src/models/user.cr
08:26:45 Generate    | new       src/controllers/registration_controller.cr
08:26:45 Generate    | new       src/controllers/user_controller.cr
08:26:45 Generate    | new       src/controllers/session_controller.cr
08:26:45 Generate    | new       src/views/registration/new.slang
08:26:45 Generate    | rewritten src/views/layouts/_nav.slang
08:26:45 Generate    | new       src/views/user/show.slang
08:26:45 Generate    | new       src/views/user/edit.slang
08:26:45 Generate    | new       src/views/session/new.slang
08:26:45 Generate    | new       src/handlers/authenticate.cr
```

To finalize installing the generated authentication system, we have to migrate the database.

```text
maze db create migrate
```

```text
08:52:25 (INFO) Database    | Created database blogsy_development
08:52:25 (INFO) Database    | Migrating db, current version: 0, target: 20180110205213147
08:52:25 (INFO) Database    | OK   20180110205213147_create_user.sql
```

Now we can run our local development server and see our working authentication system.

```text
maze watch
```

```text
08:53:52 Watcher    | Terminating app Blogsy...
08:53:52 Watcher    | Compiling Blogsy...
08:53:52 Watcher    | Building project Blogsy...
08:54:05 Server     | [Maze 0.6.1] serving application "Blogsy" at http://0.0.0.0:3000
08:54:05 Server     | Server started in development.
08:54:05 Server     | Startup Time 00:00:00.000596000
```

### 4. Sign up and Sign in Pages

To see the signup page visit [http://0.0.0.0:3000/signup](http://0.0.0.0:3000/signup)

## Recap

Maze framework provides an authentication system generator that allows you to focus on build your application rather than implementation details. The built-in authentication generator is not a full-featured authentication system, it provides the basic framework and can be extended as needed.

