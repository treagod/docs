Grip comes with a pre-defined error handlers for the JSON response type. You can customize the built-in error pages or even add your own using the `error` macro.

```ruby
class IndexController < Grip::Controllers::Http
  def get(context)
    # Pre-defined classes for specific error codes, https://github.com/grip-framework/exceptions.
    raise Exceptions::NotFound.new
  end
end

class NotFoundController < Grip::Controllers::Exception
  # To keep the structure of the project
  # we still inherit from the Base class which forces us
  # to define the default `call` function.
  def call(context)
    context
      .json(
        {
          "errors" => [context.exception.not_nil!.to_s]
        }
      )
  end
end

class ForbiddenController < Grip::Controllers::Exception
  def call(context)
    context
      .put_status(403) # Raised error automatically carries over the status code of the exception.
      .json(
        {
          "error" => ["You lack privileges to access the current resource!"]
        }
      )
  end
end

class App < Grip::Application
  def routes
    error 403, ForbiddenController
    error 404, NotFoundController

    get "/", IndexController
  end
end
```
