Grip comes with a pre-defined error handlers for the JSON response type. You can customize the built-in error pages or even add your own using the `error` macro.

```ruby
class IndexController < Grip::Controllers::Http
  def get(context : Context) : Context
    raise Grip::Exceptions::NotFound.new
  end
end

class NotFoundController < Grip::Controllers::Exception
  # To keep the structure of the project
  # we still inherit from the Base class which forces us
  # to define the default `call` function.
  def call(context : Context) : Context
    context
      .json(
        {
          "errors" => [context.exception.not_nil!.to_s]
        }
      )
  end
end

class ForbiddenController < Grip::Controllers::Exception
  def call(context : Context) : Context
    context
      .put_status(403) # Raised error automatically carries over the status code of the exception.
      .json(
        {
          "error" => ["You lack privileges to access the current resource!"]
        }
      )
  end
end

class Application < Grip::Application
  def routes
    error 403, ForbiddenController
    error 404, NotFoundController

    get "/", IndexController
  end
end
```

Keep in mind that if you won't use the `Exceptions` class this will just return as a normal response:

```ruby
class IndexController < Grip::Controllers::Http
  def get(context : Context) : Context
    context
      .put_status(404)
      .html("<p>404 Not found</p>")
      .halt
  end
end
```

and this will trigger an error handler defined in the routes method of the application:

```ruby
class IndexController < Grip::Controllers::Http
  def get(context : Context) : Context
    raise Grip::Exceptions::NotFound.new
  end
end
```

you can also raise any exception you want and handle it in the error handler like this:

```ruby
class ArgumentException < Grip::Exceptions::Base
  @status = HTTP::Status::BAD_REQUEST

  def initialize(@message : String = "Argument error")
  end
end

class IndexController < Grip::Controllers::Http
  def get(context : Context) : Context
    raise ArgumentException.new("Something went wrong")
  end
end

class BadRequestController < Grip::Controllers::Exception
  def call(context : Context) : Context
    case context.exception.not_nil!
    when Grip::Exceptions::BadRequest
      context
        .json(
          {
            id:      UUID.random.to_s,
            message: "400 Bad request",
          }
        )
    when ArgumentException
      context
        .json(
          {
            id:      UUID.random.to_s,
            message: "An argument error has occured, #{context.exception.not_nil!}",
          }
        )
    else
      context
        .halt
    end
  end
end
```
