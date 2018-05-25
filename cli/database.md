# Database

## `maze db`

The `database` or `db` command is one of the most common command that you will be operating. This command allows you to work with the database engine of choice when the Maze application was generated.

Here is a list of the commands available:

* **create** Creates the database for the environment specified in your configuration file.
* **drop**   Drops the database for the environment specified in your configuration file.
* **migrate** or **m** Migrates `up` or `down` the database version
* **rollback** Rolls back your database to a specific version or to previous version
* **redo** Repeats the database version specified or lasted version
* **status** Prints the current database migration status
* **seed** Adds initial data after a database is created
* **version** Prints the database current version.

```text
maze database [COMMANDS1 COMMANDS2...]

Arguments:
  COMMANDS (Accepts multiple)  drop create migrate rollback redo status version seed
```

## Example Usages

### **Create**

```text
$ maze db create
Created database blog_development
```

{% hint style="warning" %}
Starting with version 0.3.5 - Maze made two changes regarding databases:

* Maze will substitute hyphens `-` for underscores `_` in database names  to keep it PostgreSQL friendly.
* The default user for `pg` databases is `postgres` rather than `root`in your configuration file.

`postgres://postgres:@localhost:5432/microsecond_blog_development`
{% endhint %}

```text
$ maze new microsecond-blog
$ cd microsecond-blog
$ maze db create
Created database microsecond_blog_development
```

### **Drop**

```text
$ maze db drop
Dropped database blog_development
```

### **Migrate**

```text
$ maze db migrate
Migrating db, current version: 0, target: 20170928204246
OK   20170928204246_create_post.sql
```

### **Rollback**

```text
$ maze db rollback
Migrating db, current version: 20170928204246, target: 0
OK   20170928204246_create_post.sql
```

### **Redo**

```text
$ maze db redo
Migrating db, current version: 20170928204246, target: 0
OK   20170928204246_create_post.sql
Migrating db, current version: 0, target: 20170928204246
OK   20170928204246_create_post.sql
```

### **Status**

```text
$ maze db status
Applied At                  Migration
=======================================
2017-09-28 20:44:22 UTC  -- 20170928204246_create_post.sql
```

### **Seed**

```text
$ maze db seed
Seeded database
```

### **Version**

```text
$ maze db version
20170928204246
```

