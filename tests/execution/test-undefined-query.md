---
error: true
---

# test-undefined-query

```graphql @schema
schema @server {
  query: Query
}

type Post {
  id: Int
  user: User! @http(url: "http://jsonplaceholder.typicode.com/users", query: [{key: "id", value: "{{.value.test.id}}"}])
  nested: User!
    @http(url: "http://jsonplaceholder.typicode.com/users", query: [{key: "id", value: "{{.value.user.nested.test}}"}])
  innerNested: User!
    @http(
      url: "http://jsonplaceholder.typicode.com/users"
      query: [{key: "id", value: "{{.value.user.nested.inner.test.id}}"}]
    )
  innerIdNested: User!
    @http(
      url: "http://jsonplaceholder.typicode.com/users"
      query: [{key: "id", value: "{{.value.user.nested.inner.id.test}}"}]
    )
}

type Query {
  posts: [Post] @http(url: "http://jsonplaceholder.typicode.com/posts")
}

type Inner {
  id: Int!
}

type NestedUser {
  id: Int!
  name: String
  inner: Inner
}

type User {
  id: Int!
  name: String
  nested: NestedUser
}
```
