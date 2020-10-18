Basic authorization is based upon an Base64 encoded header present in the request.

```ruby
class Application
  def routes
    pipeline :auth, [
      Pipes::Basic.new("username", "password")
    ]
  end
end
```
