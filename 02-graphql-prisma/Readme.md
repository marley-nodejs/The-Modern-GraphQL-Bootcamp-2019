# [Udemy, Andrew Mead] The Modern GraphQL Bootcamp (Advanced Node.js) [2019, ENG]

# GraphQL Prisma

<br/>

## 05 Database Storage with Prisma

<br/>

### 05. Prisma Ubuntu Setup

heroku.com --> Create New App -->

<br/>

![Application](../img/pic-02-01.png?raw=true)

<br/>

Create App

<br/>

Overview --> Configure Addons

<br/>

![Application](../img/pic-02-02.png?raw=true)

<br/>

Ubuntu Store --> Install pgadmin

<br/>

**Install**

- docker
- docker-compose

<br/>

### 06. Prisma 101

http://prisma.io

    $ npm install -g prisma

<br/>

    $  prisma -v
    Prisma CLI version: prisma/1.34.10 (linux-x64) node-v12.13.1

<br/>

    $ cd 02-graphql-prisma/api/

<br/>

    $ prisma init prisma

    --> Use existing database
    --> PostgreSQL

    Does your database contain existing data?
    --> No

    Use SSL?
    --> Use SSL? Yes

    Select the programming language for the generated Prisma client
    --> Don't generate

<br/>

    $ cd prisma
    $ docker-compose up -d
    $ prisma deploy

http://localhost:4466/

<br/>

### 07. Exploring the Prisma GraphQL API

```
mutation {
  createUser(
    data: {
      name: "Andrey Mead"
    }
  ) {
    id,
    name
  }
}
```

<br/>

```
mutation {
  createUser(
    data: {
      name: "Vikram"
    }
  ) {
    id,
    name
  }
}
```

<br/>

```
query{
  users {
    id,
    name
  }
}
```

<br/>

```
mutation {
  updateUser(
    where: {
      id: "ck5lxfneg006b0706xaec3ind"
    },
    data: {
      name: "Andrew"
    }
  ) {
    id,
    name
  }
}
```

<br/>

```
// DELETE USER
mutation {
  deleteUser (
    where: {
      id: "ck5lxfneg006b0706xaec3ind"
    }){
    id,
    name
  }
}

```

<br/>

### 08. Add Post type to Prisma

pgadmin --> remove tables

<br/>

    $ prisma deploy

<br/>

```
mutation {
  createUser(
    data: {
      name: "Andrey Mead",
      email: "andrew@example.com"
    }
  ) {
    id,
    name
  }
}
```

<br/>

```
mutation {
  createPost(
    data: {
      title: "Prisma title",
      body: "Prisma body",
      published: false,
      author: {
        connect: {
          id: "ck5lzwfh800n90838emq6q076"
        }
      }
    }
  ){
    id,
    title,
    body,
    published,
    author {
      id,
      name
    }
  }
}
```

<br/>

### 09. Adding Comment Type to Prisma

<br/>

    $ prisma deploy

<br/>

```
query{
  users {
    id,
    name,
    posts {
      id
    }
  }
}
```

<br/>

```
mutation {
  updatePost(
    where: {
      id: "ck5m02cip00r708384cgc5bp8"
    },
    data: {
      published: true
    }
  ){
    id,
    title,
    body,
    published,
    author {
      id,
      name
    }
  }
}
```

<br/>

```
mutation {
  createUser(
    data: {
      name: "Marley",
      email: "marley@pochta.ru"
    }
  ) {
    id,
    name
  }
}
```

<br/>

```
mutation {
  createComment(
    data: {
      text: "A comment from Prisma GraphQL",
      author: {
        connect: {
          id: "ck5m0ub1a019u0838z2qtnjp6"
        }
      },
      post: {
        connect: {
          id: "ck5m02cip00r708384cgc5bp8"
        }
      }}
  )
  {
      id,
      text,
      author{
        id,
        name
      }
  }
}
```

<br/>

```
query {
  comments{
    id,
    text,
    author{
      id,
      name
    }
  }
}
```

<br/>

### 10. Integrating Prisma into a Node.js Project

https://github.com/prisma-labs/prisma-binding

    $ npm install --save prisma-binding

https://github.com/Urigo/graphql-cli

    $ npm install --save graphql-cli

<br/>

    $ npm run get-schema

<br/>

### 11. Using Prisma Bindings

    $ npm start

<br/>

**response:**

```
[
  {
    "id": "ck5lzwfh800n90838emq6q076",
    "name": "Andrey Mead",
    "email": "anrew@example.com",
    "posts": [
      {
        "id": "ck5m02cip00r708384cgc5bp8",
        "title": "Prisma title"
      }
    ]
  },
  {
    "id": "ck5m0ub1a019u0838z2qtnjp6",
    "name": "Marley",
    "email": "marley@pochta.ru",
    "posts": []
  }
]
[
  {
    "id": "ck5m14p6001go0838rl9yhjq5",
    "text": "A comment from Prisma GraphQL",
    "author": {
      "id": "ck5m0ub1a019u0838z2qtnjp6",
      "name": "Marley"
    }
  }
]

```

<br/>

### 12. Mutations with Prisma Bindings

**response**

```
***
  {
    "id": "ck69ming2002z0744utek6zy6",
    "title": "GraphQL 101!",
    "body": "This is how to get started with GraphQL...",
    "published": true
  }

```

<br/>

### 13. Using AsyncAwait with Prisma Bindings

<br/>

### 14. Checking If Data Exists Using Prisma Bindings

<br/>

### 15. Customizing Type Relationships

<br/>

    $ prisma deploy

<br/>

```
// DELETE USER
mutation {
  deleteUser (
    where: {
      id: "ck5lxfneg006b0706xaec3ind"
    }){
    id,
    name,
    email
  }
}
```

<br/>

### 16. Modeling a Review System with Prisma Set Up (Challenge description)

    $ cd ../prisma-review-website/
    $ prisma deploy

http://localhost:4466/reviews/default

<br/>

![Application](../img/pic-02-03.png?raw=true)

<br/>

### 17. Modeling a Review System with Prisma Solution (Challenge solution)

    $ cd prisma-review-website/
    $ prisma deploy

http://localhost:4466/reviews/default

<br/>

I recreated postgresql database (heroku). Because there was a strange error.

<br/>

```
mutation {
  createBook(data: {
    title: "Rest",
    author: "Alex Pang",
    isbn: "abc123"
  }) {
    id,
    title,
    author,
    isbn,
    reviews {
      id,
      text,
      rating
    }
  }
}
```

<br/>

```
mutation {
  createUser(data: {
    username: "SleepyGuy"
  }) {
    id,
    username
  }
}
```

```
mutation {
  createUser(data: {
    username: "SleepyGal"
  }) {
    id,
    username
  }
}
```

<br/>

```
query{
  users {
    id,
  	username
  }
}

```

<br/>

```
mutation {
  createReview(data:{
    text: "It was a good read!",
    rating: 5,
    book: {
      connect: {
        id: "ck6arh4vn004p07468ckj2nz8"
      }
    },
    author: {
      connect: {
        id: "ck6argu6000490746mrsvxjoc"
      }
    }
  }) {
    id,
    text,
    rating
  }
}

```

<br/>

```
mutation {
  createReview(data:{
    rating: 4,
    book: {
      connect: {
        id: "ck6arh4vn004p07468ckj2nz8"
      }
    },
    author: {
      connect: {
        id: "ck6argzgq004h0746aszfgqbm"
      }
    }
  }) {
    id,
    text,
    rating
  }
}
```

<br/>

```
query {
  books {
    id,
    title,
    author,
    isbn,
    reviews {
      id,
      text,
      rating,
      author {
        id,
        username
      }
    }
  }
}
```

<br/>

**response:**

<br/>

```
{
  "data": {
    "books": [
      {
        "author": "Alex Pang",
        "id": "ck6arh4vn004p07468ckj2nz8",
        "reviews": [
          {
            "id": "ck6asjcyk00qq0746w558ylg4",
            "text": "It was a good read!",
            "rating": 5,
            "author": {
              "id": "ck6argu6000490746mrsvxjoc",
              "username": "SleepyGuy"
            }
          },
          {
            "id": "ck6aslhrr00sa074631tweq7n",
            "text": null,
            "rating": 4,
            "author": {
              "id": "ck6argzgq004h0746aszfgqbm",
              "username": "SleepyGal"
            }
          }
        ],
        "isbn": "abc123",
        "title": "Rest"
      }
    ]
  }
}
```

<br/>

```
mutation {
  deleteUser(
    where: {
      id: "ck6argu6000490746mrsvxjoc"
    }
  ) {
    id,
    username
  }
}
```

<br/>

```
mutation {
  deleteBook(
    where: {
      id: "ck6arh4vn004p07468ckj2nz8"
    }
  ) {
    id,
    title
  }
}
```

<br/>

```
query {
  reviews{
    id
  }
}
```

<br/><br/>

---

<br/>

**Marley**

Any questions in english: <a href="https://jsdev.org/chat/">Telegram Chat</a>  
Любые вопросы на русском: <a href="https://jsdev.ru/chat/">Телеграм чат</a>
