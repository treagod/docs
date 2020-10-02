Secure headers are needed to avoid the problems which occur when the servers response can be bent to the clients will.

```ruby
class Application < Grip::Application
  def initialize
    pipeline :api, [
      Grip::Pipes::SecureHeaders.new
    ]
  end
end
```
