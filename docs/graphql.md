GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.

```crystal

module QueryType
  include GraphQL::ObjectType
  extend self

  # Add resolvers for queries
end

module MutationType
  include GraphQL::ObjectType
  extend self

  # Add resolvers for mutations
end

class Application < Grip::Application
  def schema
    # Follow the tutorial done by: https://github.com/ziprandom/graphql-crystal
    schema = GraphQL::Schema.from_schema(
      %{
        schema {
          query: QueryType,
          mutation: MutationType
        }

        type QueryType {
          posts: [PostType]
          users: [UserType]
          user(name: String!): UserType
        }

        type MutationType {
          post(post: PostInput) : PostType
        }

        input PostInput {
          author: String!
          title: String!
          body: String!
        }

        type UserType {
          name: String
          posts: [PostType]
        }

        type PostType {
          author: UserType
          title: String
          body: String
        }
      }
    )

    schema.query_resolver = QueryType
    schema.mutation_resolver = MutationType

    schema
  end

  def routes
    scope "/api" do
      forward "/graphql",
        Grip::ThirdParty::GraphQL::Processor,
        schema: schema()

      forward "/graphiql",
        Grip::ThirdParty::GraphQL::Interface,
        url: "/api/graphql"
    end
  end
end

app = Application.new
app.run
```
