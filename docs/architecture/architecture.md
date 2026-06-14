# OpenFGA High Level Architecture

* == server /
  * reads/writes -- from a -- database
* its architecture

![basic_architecture](deployment.svg)

* client application 
  * == service / calls OpenFGA
    * ways to call
      * -- via -- gRPC API
      * -- via -- HTTP API
      * -- vía -- OpenFGA's SDKs
        * -- [JavaScript](https://github.com/openfga/js-sdk/)
       * -- via -- [Python](https://github.com/openfga/python-sdk/)
     [Go](https://github.com/openfga/go-sdk/), [Java](https://github.com/openfga/java-sdk/), [.NET](https://github.com/openfga/dotnet-sdk/)), which use the HTTP API

    * ways to authenticate
      * -- via -- a shared secret
      * -- via -- client credentials flow
        * requirements: provider -- to -- obtain the OAuth client credentials
          * _Examples:_ KeyCloak, Auth0, Microsoft Entra

* requirements 
  * cluster / have an ingress 
    * _Example:_ nginx
  * database 
    * supported ones
      * Postgres
      * MySQL
      * SQLite
        * NOT use cases
          * MULTIPLE OpenFGA instances

- OpenFGA supports OTEL metrics, OTEL traces and JSON logging. These can be sent to any collector.

## Internal Architecture

![internals](internals.svg)

* ["/store" endpoints](https://openfga.dev/api/service#/Stores/CreateStore) 
  * allow
    * managing OpenFGA stores

* stores
  * == authorization model + data.
  * uses
    * isolate DIFFERENT
      * applications
      * environments
      * tenants

* [`/authorization-models` endpoint](https://openfga.dev/api/service#/Authorization%20Models/WriteAuthorizationModel)
  * allows 
    * writing NEW authorization models / define the authorization policies
*  [`/write` endpoint](https://openfga.dev/api/service#/Relationship%20Tuples/Write)
  * allows
    * writing & deleting relationship tuples / are validated & stored | configured database

- The [`/read`](https://openfga.dev/api/service#/Relationship%20Tuples/Read) endpoint allows retrieving the data stored in the database.

- The [`/check`](https://openfga.dev/api/service#/Relationship%20Queries/Check), [`/batch-check`](https://openfga.dev/api/service#/Relationship%20Queries/BatchCheck), [`/list-objects`](https://openfga.dev/api/service#/Relationship%20Queries/ListObjects), [`/list-users`](https://openfga.dev/api/service#/Relationship%20Queries/ListUsers), [`/expand`](https://openfga.dev/api/service#/Relationship%20Queries/Expand) endpoints evaluate the permission graph, reading data from the database and the cache.

The `cache` stores results from intermediate queries performed while evaluating the permission graph.

For more information about how OpenFGA evaluates the permission graph, refer to the following documents:

- [Check implementation](../check/README.md)
- [ListObjects implementation](../check/README.md)
- [ListObjects with intersection or exclusion implementation ](../list_objects/example_with_intersection_or_exclusion/example.md)
