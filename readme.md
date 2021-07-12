# Hackernews Clone Server - GraphQL

Hackernews clone following tutorial on graphql-node from [How to GraphQL](https://www.howtographql.com/graphql-js/0-introduction/)

## Installation

1. download the code 
2. cd to `../hackernews-node` directory and run `npm install`

## Query

1. to start the GraphQL Plaground run `node src/index.js`
2. visit `http://localhost:4000/`
3. in the GraphQL Playground Terminal run:
    ```
    query {
        feed {
            url
            description
        }
    }
    ```
4. the response should look something like this:
    ```
    {
        "data": {
            "feed": [
                {
                    "url": "www.graphqlconf.org",
                    "description": "An awesome GraphQL conference"
                }
            ]
        }
    }
    ```

## Mutation

### Signup

1. make sure the GraphQL Playground is still running. If not, follow steps 1-2 in the Query section
2. To create a new User, in the GraphQL Playground Terminal run: 
    ```
        mutation {
            signup(name:"Alex", email:"alex@prisma.io", password:"newpass") {
                token
                user {
                    id
                }
            }
        }
    ```
3. the response should look like this:
    ```
    {
        "data": {
            "signup": {
                "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjIsImlhdCI6MTYyNjEwNjI2MX0.ngHRgr9ir2p2P_nM5tn4B2_zm4M-lj2jjsSkxZ_yRrM",
                "user": {
                    "id": "2"
                }
            }
        }
    }
    ```

### Login

1. continue from step 3 in the Signup section
2. copy the token from the signup response
3. click `HTTP HEADERS` in the bottom left pane
4. in the small window that comes up, enter the following with _TOKEN_ replaced with the token you copied from step 2:
    ```
    {
    "Authorization": "Bearer _TOKEN_"
    }
    ```
5. now in the main pane, enter:
    ```
    mutation {
        login(email: "alice@prisma.io", password: "graphql") {
            token
            user {
                email
                links {
                    url
                    description
                }
            }
        }
    }
    ```

6. and the server should respond with:
    ```
    {
        "data": {
            "login": {
            "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsImlhdCI6MTYyNjEwMzg2NH0.begMJQOBcm-Hq-Y1WmUjmx2pw2McCzl5HXJQ-bgCV6E",
            "user": {
                "email": "alice@prisma.io",
                "links": [
                {
                    "url": "www.graphqlconf.org",
                    "description": "An awesome GraphQL conference"
                }
                ]
            }
            }
        }
    }
    ```