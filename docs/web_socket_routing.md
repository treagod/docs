WebSockets are easy to define and use thanks to the core team of the Crystal Programming Language.

```ruby
class DemoController < Grip::Controllers::WebSocket
  def on_open(context : Context)
    # Executed when a client opens a connection to the server.
  end

  def on_message(context : Context, message : String)
    # Executed when a client sends a message.
  end

  def on_ping(context : Context, message : String)
    # Executed when a client pings the server.
  end

  def on_pong(context : Context, message : String)
    # Executed when a server receives a pong.
  end

  def on_binary(context : Context, binary : Bytes)
    # Executed when a client sends a binary message.
  end

  def on_close(context : Context, error_code : HTTP::WebSocket::CloseCode | Int?, message : String)
    # Executed when a client closes the connection to the server.
  end
end

class Application < Grip::Application
  def routes
    pipeline :api, [
      Pipes::PoweredByHeader.new
    ]

    pipeline :web, [
      Pipes::SecureHeaders.new
    ]

    # WebSockets support the pipeline routing, keep in mind that
    # the `:id` URL here gives an option to fetch the `id` using the
    # `context : Context.fetch_path_params/0` function.
    scope "/" do
      pipe_through [:web, :api]

      ws "/:id", DemoController
    end
  end
end
```

Make sure to compile the application with WebSocket support:

```bash
crystal run ./src/appliaction.cr -D websocket
```
