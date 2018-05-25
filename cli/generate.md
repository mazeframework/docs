---
description: One day to design and code...
---

# Generate

The generators in maze are a great way to get an application up and running quickly. In addition, they help keep code consistent and following convention.

## Example Usage

You can always see the available generators by running `maze generate` as below:

```text
$ maze generate
Parsing Error: The TYPE argument is required.

maze generate [OPTIONS] TYPE NAME [FIELDS1 FIELDS2...]

Arguments:
  FIELDS (multiple)  user:reference name:string body:text age:integer published:bool
  NAME               name of resource
  TYPE               scaffold, model, controller, migration, mailer, socket, channel, auth

Options:
  --no-color  Disable colored output
```

Generators can be used multi-word names, the class names will be `CamelCase` and file names will be `snake_case`, the command line input can be either:

```text
$ maze generate [TYPE] MultiWordName [FIELD1 FIELD2 ...]
# OR
$ maze generate [TYPE] multi_word_name [FIELD1 FIELD2 ...]
```

See [Scaffolding](generate.md#scaffolding) below for full example.

Examples of Usage

* [Scaffolding](generate.md#scaffolding)
* [Auth](generate.md#auth)
* [Model](generate.md#model)
* [Controller](generate.md#controller)

### Scaffolding

Scaffolding will create the model \(and specs\), views, controller \(and specs\) and migrations for a resource. Additionally, it will add the new resource to the nav bar and

```text
$ maze generate scaffold Post title body:text
Rendering Scaffold post
new       db/migrations/20171114103058417_create_post.sql
new       spec/models/spec_helper.cr
new       spec/models/post_spec.cr
new       src/models/post.cr
new       spec/controllers/spec_helper.cr
new       spec/controllers/post_controller_spec.cr
new       src/controllers/post_controller.cr
rewritten src/views/layouts/_nav.slang
new       src/views/post/_form.slang
new       src/views/post/edit.slang
new       src/views/post/index.slang
new       src/views/post/new.slang
new       src/views/post/show.slang
```

If you scaffold a multi-word resource, the class names will be `CamelCase` and file names will be `snake_case`, the command line input can be either:

```text
$ maze generate scaffold PostComment post:reference body:text
# OR
$ maze generate scaffold post_comment post:reference body:text
Rendering Scaffold post_comment
new       db/migrations/20171114103306763_create_post_comment.sql
skipped   spec/models/spec_helper.cr
new       spec/models/post_comment_spec.cr
new       src/models/post_comment.cr
skipped   spec/controllers/spec_helper.cr
new       spec/controllers/post_comment_controller_spec.cr
new       src/controllers/post_comment_controller.cr
rewritten src/views/layouts/_nav.slang
new       src/views/post_comment/_form.slang
new       src/views/post_comment/edit.slang
new       src/views/post_comment/index.slang
new       src/views/post_comment/new.slang
new       src/views/post_comment/show.slang
```

### Auth

```text
$ maze g auth User
Rendering Auth user
new       db/migrations/20171019214851_create_user.sql
new       db/seeds.cr
new       spec/controllers/spec_helper.cr
new       spec/models/spec_helper.cr
new       spec/models/user_spec.cr
new       src/controllers/registration_controller.cr
new       src/controllers/session_controller.cr
new       src/handlers/authenticate.cr
new       src/models/user.cr
rewritten src/views/layouts/_nav.slang
new       src/views/registration/new.slang
new       src/views/session/new.slang
```

### Model

```bash
$ maze g model Person name:string age:integer
Rendering Model person
new       db/migrations/20171019214940_create_person.sql
skipped   spec/models/spec_helper.cr
new       spec/models/person_spec.cr
new       src/models/person.cr
```

### Controller

```bash
$ maze g controller Person index:get show:get create:post update:patch
Rendering Controller person
skipped   spec/controllers/spec_helper.cr
new       spec/controllers/person_controller_spec.cr
new       src/controllers/person_controller.cr
```

## Recipes

Recipes are available to generate Scaffolding, Controller and Model artifacts in ways that vary from the standard built in generator. See the [Recipes](recipes.md) option of the Command Line Tool for more information about using recipes to generate applications.

