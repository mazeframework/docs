# Minimal Configuration

Maze can be run from a single file for minimal configuration setups if the user prefers this for smaller applications.

```ruby
require "maze"

class HelloController < Maze::Controller::Base
  def index
    "hello world"
  end
end

Maze::Server.configure do |app|
  pipeline :api do
  end

  routes :api do
    get "/", HelloController, :index
  end
end

Maze::Server.start
```

