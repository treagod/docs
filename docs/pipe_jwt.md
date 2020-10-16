JWT authorization is based upon an `Authorization` header present in the request.

```ruby
class DemoController < Grip::Controllers::Http
  def get(context)
    context
      .json(
        {
          "decoded" => context.assigns.jwt,
        }
      )
  end
end

class Application < Grip::Application
  def routes
    pipeline :api, [
      Grip::Pipes::Jwt.new
    ]

    get "/", DemoController, via: :api
  end
end
```

You can configure the JWT pipe by:

```ruby
Grip::Pipes::Jwt.new(
  secret_key: "CoolSecret!@#$%^&*()_+",
  claims: {
    :aud => "Authorization",
    :iss => "MyCoolCompany LLC.",
    :sub => nil
  },
  algorithm: JWT::Algorithm::HS256
)
```

You can use the encode and decode functions like this:

```ruby
# Keep in mind that you can still change the algorithm and secret_key by supplying the variables to the function.

#
# For example:
#   include Pipes::Twj
#   encode_and_sign(
#     data: {
#       "id" => 1
#     },
#     secret_key: "MyCoolKey",
#     algorithm: JWT::Algorithm::HS256
#   )
#

include Pipes::Twj

encode_and_sign(
  data: {
    "id" => 1
  }
)
```

```ruby
# Keep in mind that you can still change the algorithm and secret_key by supplying the variables to the function.

#
# For example:
#   include Pipes::Twj
#   decode_and_verify(
#     data: "eyOinniewi==",
#     claims: {
#       :aud => "Nothing",
#       :iss => "NoOne",
#       :sub => nil
#     },
#     secret_key: "MyCoolKey",
#     algorithm: JWT::Algorithm::HS256
#   )
#

include Pipes::Twj

decode_and_verify(
  data: "eyOnwindOWNIRnoninWINR==" # This is not valid JWT.
)
```
