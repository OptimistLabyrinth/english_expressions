# Project English Expressions

#### I store useful or interesting english expressions that I met while I'm studying english.

---

# API Design

`! (exclamation mark)` after the type means `Non-Null`

### Create

```graphql
input {
  expression: string!
  meaning: string!
  similar_meaning: [string!]!
}
```

```graphql
output {
  # field `msg` shows the result of the operation
  # success: 'OK'
  msg: string!
}
```

### Read All

```graphql
input {
   # None
}
```

```graphql
output {
  # if the operation succeed, it responds with the data as 'result' and OK as 'msg'
  result: [EachResultReadAll]
  # if the operation has any error, it responds with msg that summarizes the error
  msg: String!
}

type EachResultReadAll {
  id: int!
  expressions: string!
  meaning: string!
  similar_meaning: [string!]!
}
```

### Read One

```graphql
input {
  id: int!
}
```

```graphql
output {
  result: EachResultReadOne
  msg: string!
}

type EachResultReadOne {
  id: int!
  expressions: string!
  # links has several links that show the definition of the expression
  # field 'expressionsLinks' can have from 0 to N links
  expressionsLinks: ExpressionLinksReadOne
  meaning: string!
  similar_meaning: [EachSimilarMeaningReadOne!]!
}

type ExpressionLinksReadOne {
  # https://dictionary.cambridge.org/
  cambridge: string
  # https://www.dictionary.com/
  dictionaryDotCom: string
  # https://www.merriam-webster.com/
  merriamWebster: string
  # https://en.dict.naver.com/
  naver: string
}

type EachSimilarMeaningReadOne {
  expression: string!
  expressionLinks: ExpressionLinksReadOne
}
```

### Edit One

```graphql
input {
  id: int!
  # all the fields except id are optional
  # so only the updated field is included in the request body
  expression: string
  expressionsLinks: ExpressionLinksEditOne
  meaning: string
  similar_meaning: [EachSimilarMeaningEditOne!]
}

type ExpressionLinksEditOne {
  cambridge: string
  dictionaryDotCom: string
  merriamWebster: string
  naver: string
}

type EachSimilarMeaningEditOne {
  expression: string!
  expressionLinks: ExpressionLinksEditOne
}
```

```graphql
output {
  msg: string!
}
```

### Delete Many

```graphql
input {
  ids: [int!]!
}
```

```graphql
output {
  msg: string!
}
```
