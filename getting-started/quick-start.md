# Quick Start

This quick start guide will help you get a full stack web application running in just a few minutes by leveraging maze’s code generators.

It will take us just 7 steps. Let’s get started!

![Let&#x2019;s get started!](https://github.com/mazeframework/mazeframework.github.io/blob/master/assets/images/maze.svg)

## 1. Install dependencies

{% hint style="info" %}
If you already have `crystal`, `maze`, and a database installed, you can [skip this step](quick-start.md#2-generate-a-new-maze-application).
{% endhint %}

### 1.1 Install `crystal` and `maze`

Instructions for OS X using homebrew and Debian/Ubuntu are below. See full installation instructions [here](https://crystal-lang.org/docs/installation/) for RedHat & CentOS, ArchLinux & Derivatives, and more complete instructions.

#### OS X with homebrew

Installing crystal with homebrew

```text
brew update
brew install crystal-lang
```

#### Ubuntu or Debian

First install crystal and required libraries

```text
curl https://dist.crystal-lang.org/apt/setup.sh | sudo bash
sudo apt-get install -y build-essential crystal git libreadline-dev libsqlite3-dev libpq-dev libmysqlclient-dev libssl-dev libyaml-dev
```

Then install maze \(from github\)

```text
sudo apt-get install
git clone https://github.com/mazeframework/maze.git
cd maze/
shards build maze
sudo cp bin/maze /usr/local/bin
```

{% hint style="info" %}
Above are the steps for building from source, the dependencies are specific to Ubuntu/Debian. See [full installation instructions](../guides/installation.md) for other Linux Distributions.
{% endhint %}

### 1.2 Install a database

Maze works with `postgresql` \(default\), `mysql`, or `sqlite`.

If you don’t already have one of these installed, please follow the guides provided by each database maintainer:

* [Postgresql Installation Guides](https://wiki.postgresql.org/wiki/Detailed_installation_guides)  
* [MySQL Installation Guides](https://dev.mysql.com/doc/refman/8.0/en/installing.html)  
* [Tutorial on installing SQLite](https://www.tutorialspoint.com/sqlite/sqlite_installation.htm)  

{% hint style="info" %}
On OS X any of the databases can be installed with `brew install [database]`
{% endhint %}

## 2. Generate a new Maze application

With all dependencies successfully installed, we can generate a new application with `maze new`

After the code for the new application is generated, we will `cd` into the new directory and execute a `shards install`.

The shards install command may take a little while - it has to download all shard dependencies.

{% hint style="info" %}
The default setup will use a postgresql database, use `-d mysql` or `-d sqlite` for mysql and sqlite, respectively.
{% endhint %}

```text
maze new pet-tracker
cd pet-tracker
shards install
```

## 3. Generate a resource

With the skeleton application generated, we can generate our first RESTful resource.

The `maze generate scaffold` command will help us do this.

{% hint style="info" %}
`g` is shorthand for `generate`
{% endhint %}

```text
maze g scaffold Pet name:string breed:string age:integer
```

## 4. Create and migrate the database

Generating the application and the scaffolded resource provides the configuration and migration files needed to setup our database.

`maze db` will help us do this.

```text
maze db create migrate
```

This will create a new database and run the migration to create a `pets` table with the specified columns.

## 5. Build the application and run the server

We can use `maze watch` to both build the binary application and start the server. Additionally, `maze watch` will detect code changes then recompile and restart the application automatically.

```text
maze watch
```

## 6. Use your brand new web application!

Open any browser and goto [http://localhost:3000](http://localhost:3000) You should see a home page load and “Pets” in the nav bar. If you click on the “Pets” link, you should be able to perform all 7 RESTful actions for the “pets” resource.

## 7. Deploy your web application

{% page-ref page="../deployment/" %}

## List of Commands

You can use these commands to create new awesome applications :-\)

```text
maze new pet-tracker
cd pet-tracker
shards install
maze generate scaffold Pet name:string breed:string age:integer
maze db create migrate
maze watch
```

## Demo

Here is a demo and the source code is available on [Github](https://github.com/faustinoaq/pet-tracker).

![Quick Start Demo](https://raw.githubusercontent.com/amberframework/site-assets/master/videos/quick-start-demo.gif)
