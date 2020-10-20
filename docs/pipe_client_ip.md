Client IP address is needed for tracking the requests, filtering blacklisted addresses and creating an authorization scheme for certain IP addresses.

```ruby
class DemoController < Grip::Controllers::Http
  def get(context)
    puts context.asssigns.client_ip

    context
      .json("Hello, World!")
  end
end

class Application < Grip::Application
  def routes
    pipeline :api, [
      Pipes::ClientIp.new
    ]

    scope "/" do
      pipe_through :api

      get "/", DemoController
    end
  end
end
```
