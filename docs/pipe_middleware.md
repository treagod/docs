Pipe middleware is the building block of the framework, some helpful pipes are included with the framework.

Creating a custom pipe is as easy as creating an `HTTP handler`:

```ruby
class DemoPipe < Pipes::Base
  def call(context : HTTP::Server::Context) : HTTP::Server::Context
    # Mutate the context and pass it on to the next handler.
  end
end

class DemoController < Grip::Controllers::Http
  def get(context : Context) : Context
    context
      .json("Hello, World!")
  end
end

class Application < Grip::Application
  def routes
    # Creating a pipeline with a single pipe to be routed through.
    pipeline :web, [
      DemoPipe.new
    ]

    scope "/" do
      pipe_through :web

      get "/", DemoController
    end
  end
end
```

Advantage of the pipe over a raw middleware is that you can controll which routes go through the middleware and which don't.
