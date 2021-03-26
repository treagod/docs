Forward forwards a request to a specific route, mainly a HTTP::Handler class.

```ruby
class Authorization
  include HTTP::Handler

  def initialize(@username : String, @password); end

  def call(context)
    context
  end
end

class Application < Grip::Application
  def routes
    forward "/", Authorization, username: "admin", password: "admin"
  end
end
```



