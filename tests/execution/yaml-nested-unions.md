# Using union types inside other union types

```yml @config
schema:
  query: Query

types:
  T1:
    fields:
      t1:
        type:
          name: String
  T2:
    fields:
      t2:
        type:
          name: Int
  T3:
    fields:
      t3:
        type:
          name: Boolean
      t33:
        type:
          name: Float
          required: true

  T4:
    fields:
      t4:
        type:
          name: String

  T5:
    fields:
      t5:
        type:
          name: Boolean

  Query:
    fields:
      test:
        type:
          name: U
        args:
          u:
            type:
              name: U
              required: true
        http:
          url: http://localhost/users/{{args.u}}

unions:
  U1:
    types: ["T1", "T2", "T3"]
  U2:
    types: ["T3", "T4"]
  U:
    types: ["U1", "U2", "T5"]
```
