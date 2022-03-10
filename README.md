## Read the full tutorial at
- https://robmellett.com/posts/laravel-and-hasura-for-instant-graphql

## Hasura CLI
Install the Hasura CLI
- https://hasura.io/docs/latest/graphql/core/hasura-cli/install-hasura-cli.html

## Hasura Documentation
- https://hasura.io/docs/latest/graphql/core/databases/postgres/queries/index.html
- https://hasura.io/blog/graphql-and-tree-data-structures-with-postgres-on-hasura-dfa13c0d9b5f/
- https://hasura.io/docs/latest/graphql/core/databases/postgres/queries/variables-aliases-fragments-directives.html
- https://hasura.io/docs/1.0/graphql/core/auth/authorization/common-roles-auth-examples.html#anonymous-not-logged-in-users

## Laravel Setup
1. Copy the `.env.example` to `.env`
2. Run `composer install` on your local machine
3. If you are running the project on a Mac M1, you might need to update the `docker-compose.yml` to be like the following

```dockerfile
graphql-engine:
    ## On a Mac M1, you might need to enable this line
    image: fedormelexin/graphql-engine-arm64:v2.0.9.cli-migrations-v3
```
4. Start the docker containers with Laravel Sail `sail up -d`
5. Run the laravel migrations with `sail artisan migrate:fresh --seed`

#### Important: 
If you are starting the project for the first time, Laravel will not have run the migrations, so the graphql server might have trouble loading, or the GraphQL server may have an error like:

`You have been redirected because your GraphQL Engine metadata is in an inconsistent state`.  

Make sure you run `sail artisan migrate:fresh --seed`, and restart the docker containers.

## Managing the Hasura Data
1. The configuration is stored in the `hasura` directory.
2. When making changes to the graphql schema / metadata configuration, you will need to make sure it is stored.

Note: Make sure you have installed the Hasura CLI.

```shell
cd hasura
hasura metadata export
```

## Helpful Docker Commands
If you need to detach the docker database volume
```shell
docker-compose down --volume
```

If you need to delete and remove all Docker volumes. You might need to
use this to fully reset the database to a clean state.
```shell
docker volume rm $(docker volume ls -q)
```

