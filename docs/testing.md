1.Add spec-grip to your shard.yml file as a dependencie.

```yaml
dependencies:
  grip:
    github: grip-framework/grip

  spec-grip:
    github: grip-framework/spec-grip
```

2.Then run shards to get the dependencies:

```bash
$ shards install
```

3.Now you should require it before your files in your spec/spec_helper.cr

```
require "spec-grip"
require "../src/your-grip-app"
```

For example, your Grip application:

```ruby
# src/your-grip-app.cr

require "grip"

class Index < Grip::Controllers::Http
  def get(context)
    context
      .text("Hello, World!")
  end
end

class Application < Grip::Application
  def initialize
    get "/", Index
  end
end

app = Application.new
app.run
```

4.Now you can easily test your Grip application in your specs.

```bash
APP_ENV=test crystal spec
```

```ruby
# spec/your-grip-app-spec.cr

describe "Your::Grip::App" do
  # You can use get,post,put,patch,delete to call the corresponding route.
  it "renders /" do
    get "/" do |response|
      response.body.should eq "Hello, World!"
    end
  end
end
```
