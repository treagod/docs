Parameter validation is only supported for the JSON parameters.

```ruby
class DemoController < Grip::Controllers::Http
  def post(context : Context) : Context
    parameters =
      # A named tuple which has the types and variable names pre-defined.
      Parameters(first_name: String, last_name: String, email: String, password: String)
        # Load the information from a JSON parameter body.
        .form(context.fetch_json_params)
          # Validate the string containing only alpha characters, if the block returns false an error is raised.
          .valid?(:first_name) { |value| value.alpha? }
          .valid?(:last_name) { |value| value.alpha? }
          .valid?(:email) { |value| value.email? }
          .valid?(:password) { |value| value.alphanum? && value.size >= 8 }

    context
      .json(
        parameters
      )
  end
end
```

There are custom methods included from extension modules located in the extension folder of the Grip framework, which provide additional validation functionality to the native data structures.
