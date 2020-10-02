Powered by header provides a pipe which allows you to respond with a header containing information about the server.

```ruby
class Application < Grip::Application
  def initiialize
    pipeline :api, [
      Grip::Pipes::PoweredByHeader.new
    ]
  end
end
```
