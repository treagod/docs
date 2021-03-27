Forward forwards a request to a specific route, mainly a HTTP::Handler class.

```ruby
class Authorization < Grip::Controllers::Base
  def initialize(@username : String, @password); end

  def call(context : Context) : Context
    context
  end
end

class Application < Grip::Application
  def routes
    # Forward macro simply routes the matched requests to a certain Base controller
    # which contains a single call/1 function.
    forward "/", Authorization, username: "admin", password: "admin"
  end
end
```



