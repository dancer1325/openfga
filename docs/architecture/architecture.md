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

    * Calls to the OpenFGA API can be authenticated using a shared secret or through a client credentials flow. If the application uses client credentials, it needs to obtain those for an OAuth client credentials provider (KeyCloak, Auth0, Microsoft Entra etc). 
- The cluster needs to have an ingress for load balancing (e.g. nginx).
- The OpenFGA service needs a database. At the time of writing the supported ones are Postgres, MySQL and SQLite. SQLite is not designed for multiple instances of OpenFGA.
- OpenFGA supports OTEL metrics, OTEL traces and JSON logging. These can be sent to any collector.

## Internal Architecture

The following diagram describes at high level how OpenFGA works internally. 

![internals](internals.svg)

- The [`/store`](https://openfga.dev/api/service#/Stores/CreateStore) endpoints allow managing OpenFGA stores, which contain the authorization model + the data. Stores can be used for isolating different applications, environments, or tenants.

- The [`/authorization-models`](https://openfga.dev/api/service#/Authorization%20Models/WriteAuthorizationModel) endpoint allows writing new authorization models, which define the authorization policies.

 - The [`/write`](https://openfga.dev/api/service#/Relationship%20Tuples/Write) endpoint allows writing and deleting relationship tuples, which are validated and stored in the configured database.

- The [`/read`](https://openfga.dev/api/service#/Relationship%20Tuples/Read) endpoint allows retrieving the data stored in the database.

- The [`/check`](https://openfga.dev/api/service#/Relationship%20Queries/Check), [`/batch-check`](https://openfga.dev/api/service#/Relationship%20Queries/BatchCheck), [`/list-objects`](https://openfga.dev/api/service#/Relationship%20Queries/ListObjects), [`/list-users`](https://openfga.dev/api/service#/Relationship%20Queries/ListUsers), [`/expand`](https://openfga.dev/api/service#/Relationship%20Queries/Expand) endpoints evaluate the permission graph, reading data from the database and the cache.

The `cache` stores results from intermediate queries performed while evaluating the permission graph.

For more information about how OpenFGA evaluates the permission graph, refer to the following documents:

- [Check implementation](../check/README.md)
- [ListObjects implementation](../check/README.md)
- [ListObjects with intersection or exclusion implementation ](../list_objects/example_with_intersection_or_exclusion/example.md)
