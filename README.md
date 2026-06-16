![OpenFGA Logo](./openfga-logo.png)
# OpenFGA

* **OpenFGA**
  * == authorization/permission engine /
    * focus
      * high-performance
      * reliability
    * flexible storage backends
      * In-Memory
      * PostgreSQL
      * MySQL
      * SQLite beta
    * -- based on -- [Google Zanzibar](https://research.google/pubs/pub48190/)
    * open source
  * allows
    * about fine-grained access control
      * easily model 
      * enforce | their applications
  * -- created by -- Auth0 FGA team
  * audience
    * application builders
      * == | applications, add fine-grained authorization
  * provide
    * API (HTTP API % gRPC)
    * SDKs 
      * [JavaScript](https://github.com/openfga/js-sdk)
      * [GoLang](https://github.com/openfga/go-sdk)
      * [.NET](https://github.com/openfga/dotnet-sdk)
      * [Node.js](https://www.npmjs.com/package/@openfga/sdk)
      * [Python](https://github.com/openfga/python-sdk)
      * [Java](https://central.sonatype.com/artifact/dev.openfga/openfga-sdk)
    * [CLI](https://github.com/openfga/cli)
      * uses
        * interact -- with an -- OpenFGA server
        * [test authorization models](https://openfga.dev/docs/modeling/testing) 
    * [Terraform Provider](https://github.com/openfga/terraform-provider-openfga)
      * uses
        * configure OpenFGA servers -- as -- code 
  * [Playground](https://openfga.dev/docs/getting-started/setup-openfga/playground)
  * can be embedded -- as a -- [Go library](https://pkg.go.dev/github.com/openfga/openfga/pkg/server#example-NewServerWithOpts) 
  * [Adopters](https://github.com/openfga/community/blob/main/ADOPTERS.md)

## Quickstart


* [how to configure](docs/getting-started/setup-openfga/configure-openfga) 
  * storage backends
  * tuning performance
* [how to deploy OpenFGA securely | production](docs/getting-started/running-in-production)

## Playground

* lets you 
  * about authorization setups
    * model
    * visualize
    * test 
* by default,
  * | http://localhost:3000/playground
* use cases
  * local development

TODO: 
> It can currently only be configured to connect to an OpenFGA server running on `localhost`.

Disable it with:

```shell
./openfga run --playground-enabled=false
```

Change port:

```shell
./openfga run --playground-enabled --playground-port 3001
```

> [!TIP]
> The `OPENFGA_HTTP_ADDR` environment variable can be used to configure the address at which the Playground expects the OpenFGA server to be.
>
> For example:
>
> ```shell
> docker run -e OPENFGA_PLAYGROUND_ENABLED=true \
> -e OPENFGA_HTTP_ADDR=0.0.0.0:4000 \
> -p 4000:4000 -p 3000:3000 openfga/openfga run
> ```
>
> This starts OpenFGA on port 4000 and configures the Playground accordingly.


## Limitations

### MySQL Storage engine

* MySQL storage engine 
  * vs other backends,
    * | tuple properties, 
      * [has stricter length limits](docs/getting-started/setup-openfga/docker#configuring-data-storage)

## Contributing & Community

* [here](https://openfga.dev/docs/community)
