# `/internal`

Private application and package code. This code never gets exported to other applications or packages and is enforced by the Go compiler. You are not limited to the top level `internal` directory. You can have more than one `internal` directory at any level in the codebase tree.

It is typical to provide an internal package named the same as the `cmd`
importing it. Example: The `cmd/foo` binary imports at least the
`/internal/foo` package for its core logic.

Examples:

* https://github.com/hashicorp/terraform/tree/master/internal
* https://github.com/influxdata/influxdb/tree/master/internal
* https://github.com/perkeep/perkeep/tree/master/internal
* https://github.com/jaegertracing/jaeger/tree/master/internal
* https://github.com/moby/moby/tree/master/internal
* https://github.com/satellity/satellity/tree/master/internal

## `/internal/pkg`

Examples:

* https://github.com/hashicorp/waypoint/tree/main/internal/pkg
