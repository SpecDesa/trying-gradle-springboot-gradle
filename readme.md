# How it was done

1.  Went to : https://start.spring.io

    1. java, 17, gradle, spring web + spring graphql, unzip and go!
    2. change settings cmd+shift+p preferences: open settings (ui) -> search for java.import.gradle.java.home and input /usr/local/Cellar/openjdk/19.0.2/ or other version.
    3. may need this in settings file to for intellisense:
       1. settings.json or settings
       2. "java.configuration.runtimes": \[
          { "name": "JavaSE-19", "path": "/usr/local/Cellar/openjdk/19.0.2" } \]

2.  add schema

    1. src/main/resources/graphql
       - Every GraphQL schema has a top-level Query type, and the fields under it are the query operations exposed by the application.
    2. add type Query, Book, Author with fields.
    3.

3.  Create the Book and Author data sources
    1. create record book and author
4.  fetch data controller

    1. Create BookController
    2. create a Querymapping
       - By defining a method named bookById annotated with @QuerMapping, this controller declares how to fetch a Book as defined under the Query type (step 2.1)
    3. Create SchemaMapping
       - annotation maps a handler method to a field in the GraphQL schema and declares it to be the DataFetcher for that field. The field name defaults to the method name, and the type name defaults to the simple class name of the source/parent object injected into the method

5.  running / testing queries

    1. create fiLE `application.properties`
    2. add `application.properties`
    3. run :

    ```query bookDetails {
    bookById(id: "book-1") {
        id
        name
        pageCount
            author {
                id
                firstName
                lastName
            }
        }
    }
    ```

6.  TEST
    1. Create BookControllerTest.java in "src/test/java/com/bp/graphql/BookControllerTests.java"
    2. Create the query for testing with a paramterized $id in src/test/resources/graphql-test/bookDetails.graphql
    3. if something wrong check spelling of folders and use test dashboard file:///Users/danieleystberg/Documents/Learning/BP/graphql/build/reports/tests/test/classes/com.bp.graphql.BookControllerTests.html#shouldGetFirstBook() and
       http://localhost:8080/graphiql?path=/graphql to see expected data and so on.
