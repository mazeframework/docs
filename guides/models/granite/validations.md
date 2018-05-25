# Validations

{% hint style="info" %}
This section is based on [Granite's README](https://mazeframework.gitbook.io/granite)
{% endhint %}

## Errors

All database errors are added to the `errors` array used by Granite::ORM::Validators with the symbol ':base'

```ruby
post = Post.new
post.save
post.errors[0].to_s.should eq "ERROR: name cannot be null"
```

## Custom validations

If you require to add more data validation to your model, you can do so by using the `validate` method.

`validate` method can be used to validate the whole object or an attribute of the object. These validations are not automatically checked when you save, to do so you need to run the `.valid?` method.

{% hint style="info" %}
Failing the validation does not prevent the object from being persisted \(saved\).
{% endhint %}

### To validate whole object

```ruby
validate(message : String, block)
```

Example:

```ruby
require "granite_orm/adapter/sqlite"

class Comment < Granite::ORM::Base
  adapter sqlite

  table_name comments
  field name : String
  field body : String

  validate("Invalid Comment.", ->(comment : self) {
    (comment.name != nil && comment.name != "") || (comment.body != nil && comment.body != "")
  })
end
```

### To validate a field in an object

```ruby
validate(name : Symbol, message : String, block)
```

Example:

```ruby
require "granite_orm/adapter/sqlite"

class Comment < Granite::ORM::Base
  adapter sqlite

  table_name comments
  field name : String
  field body : String

  validate(:name, "Name required.", ->(comment : self) {
    (comment.name != nil && comment.name != "")
  })
end
```

