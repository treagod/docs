WebSockets are easy to define and use thanks to the core team of the Crystal Programming Language.

```ruby
class DemoController < Grip::Controllers::WebSocket
  def on_open(ctx, sock)
    # Executed when a client opens a connection to the server.
  end

  def on_message(ctx, sock, msg)
    # Executed when a client sends a message.
  end

  def on_ping(ctx, sock, ping)
    # Executed when a client pings the server.
  end

  def on_pong(ctx, sock, pong)
    # Executed when a server receives a pong.
  end

  def on_binary(ctx, sock, bin)
    # Executed when a client sends a binary message.
  end

  def on_close(ctx, sock, err_code, err)
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
    # `context.fetch_path_params/0` function.
    ws "/:id", DemoController, via: [:web, :api]
  end
end
```
