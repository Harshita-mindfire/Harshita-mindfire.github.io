---
id: y0EPDmDOTZpC9TooOlWrC
title: GitHub Graphql API
desc: ''
updated: 1627977193749
created: 1627976624538
---

In my initial days, I had a hard time figuring out these queries while I was working on a task. I had used [octokit](https://www.npmjs.com/package/@octokit/graphql) for making the request.



*Graphql queries*

- Total issue count:

```graphql
query { 
  repository(owner:"dendronhq", name:"dendron") { 
    issues {
      totalCount
    }
  }
}
```

- Open and closed issue count
```graphql
query { 
  repository(owner:"dendronhq", name:"dendron") { 
    open: issues(states:OPEN) {
      totalCount
    }
    closed: issues(states:CLOSED) {
      totalCount
    }
  }
}
```

Result 
```json
{
  "data": {
    "repository": {
      "open": {
        "totalCount": 271
      },
      "closed": {
        "totalCount": 448
      }
    }
  }
}
```

- quering repository

```graphql

query { 
  repository(owner:"dendronhq", name:"dendron") { 
    issues(last:100,states:OPEN) {
       edges {
        node {
          title
          url
          number
          state
          labels(first:5) {
            edges {
              node {
                name
              }
            }
          }
          body
        }
      }
    }
  }
}
```

- search query let you search between a datetime

```graphql
{
  search(query: "repo:dendronhq/dendron is:issue is:open created:2021-06-28..2021-06-30", type: ISSUE, last: 100) {
    edges {
      node {
        ... on Issue {
        title
          url
          createdAt
          number
          state
         
        }
      }
    }
  }
}
```
- search query to get issue count

```graphql
{
  search(query: "repo:dendronhq/dendron is:issue is:open created:2021-06-28..2021-06-30", type: ISSUE, last: 100) {
    issueCount
  }
}
```



 

  ## Cursor and pagination
```graphql
 {
  search(query: "repo:dendronhq/dendron is:issue is:open created:2021-06-28..2021-06-30", type: ISSUE, first:100, after: [end_cursor_val] ) {
    pageInfo {
      startCursor
      hasNextPage
      endCursor
    }
    edges {
      cursor
      node {
        ... on Issue {
        title
          url
          createdAt
          number
          state
         
        }
      }
    }
  }
}
```

## Mutation

- Query all the labels of dendron:

```graphql
query { 
  repository(owner:"dendronhq", name:"dendron") { 
    labels(last: 100) {
      edges{
        node {
          id
          name
        }
      }
    }
}
}
```


- to update state of an issue
```graphql
mutation{
  updateIssue(input: {id : "MDU6SXNzdWU5NTI4MjU3NzY=" , state: OPEN}){
    issue {
          number
        }
  }
}
```

- with label ids:
```graphql
mutation{
  updateIssue(input: {id : "MDU6SXNzdWU5NTI4MjU3NzY=" , state: OPEN, labelIds: "MDU6TGFiZWwzMDg4MjQzMDM3" }){
    issue {
          number,
      labels(first:2)  {
        edges {
        node {
          id
          name
        }
        }
      }
        }
  }
}
```

- updating multiple labels : 

```graphql
mutation{
  updateIssue(input: {id : "MDU6SXNzdWU5NTI4ODE2Nzc" , state: CLOSED, labelIds: ["MDU6TGFiZWwzMjAxNTExMTMw", "MDU6TGFiZWwxOTY1MzE3NzI1", "MDU6TGFiZWwxOTY1MzE3NzI0"]}){
    issue {
          number,
      labels(first:4)  {
        edges {
        node {
          id
          name
        }
        }
      }
        }
  }
}
```


