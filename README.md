# Graphql API with Node.js, PostgreSQL with Prisma

> A Basic Node.js project

## Build Setup

```bash
# install dependencies
npm install

```

## Prerequisites

- Nodejs
- Postgresql

### Create and seed the database

```
npx prisma migrate dev --name init --preview-feature
```

Now, seed the database with the sample data in [`prisma/seed.ts`](./prisma/seed.ts) by running the following command:

```
npx prisma db seed --preview-feature
```

### Start the GraphQL server

Launch your GraphQL server with this command:

```
npm run dev
```

Navigate to [http://localhost:4000](http://localhost:4000) in your browser.

## Using the GraphQL API

**Request:**

### Retrieve all published posts and their authors

```graphql
query {
  feed {
    id
    title
    content
    published
    author {
      id
      name
      email
    }
  }
}
```

### Retrieve the drafts of a user

```graphql
{
  draftsByUser(userUniqueInput: { email: "mahmoud@prisma.io" }) {
    id
    title
    content
    published
    author {
      id
      name
      email
    }
  }
}
```

### Create a new user

```graphql
mutation {
  signupUser(data: { name: "Sarah", email: "sarah@prisma.io" }) {
    id
  }
}
```

### Create a new draft

```graphql
mutation {
  createDraft(
    data: { title: "Join the Prisma Slack", content: "https://slack.prisma.io" }
    authorEmail: "alice@prisma.io"
  ) {
    id
    viewCount
    published
    author {
      id
      name
    }
  }
}
```

### Publish/unpublish an existing draft

```graphql
mutation {
  togglePublishPost(id: 5) {
    id
    published
  }
}
```

### Increment the view count of a post

```graphql
mutation {
  incrementPostViewCount(id: 5) {
    id
    viewCount
  }
}
```

### Search for posts that contain a specific string in their title or content

```graphql
{
  feed(searchString: "prisma") {
    id
    title
    content
    published
  }
}
```

### Paginate and order the returned posts

```graphql
{
  feed(skip: 2, take: 2, orderBy: { updatedAt: desc }) {
    id
    updatedAt
    title
    content
    published
  }
}
```

### Retrieve a single post

```graphql
{
  postById(id: 5) {
    id
    title
    content
    published
  }
}
```

### Delete a post

```graphql
mutation {
  deletePost(id: 5) {
    id
  }
}
```
