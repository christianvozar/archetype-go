# Standard Go Codebase Layout

Go development offers some opinions such as code formatting via gofmt or golint. Go lacks cohesive opinions on the organization of code within a repository unlike a Ruby on Rails project. However, there are some layout patterns the Go compiler enforces such as packages in the /internal directory for code you do not wish to export.

This standard codebase layout follows a set of historical patterns that have emerged from the official Go standard library, official Google supported Go packages, and prominent Go projects in the ecosystem.

This codebase layout is intended to be generic but uniform. If you do not require a particular directory or pattern for your application after forking then feel free to remove it.

`/`

The root of the git repository should have almost nothing within it save a Makefile, code license, appropriately documented README, and the vendor management lock such as `go.mod`. This serves to cleanly identify the codebase is of a standard layout and won't distract the engineer from finding the appropriate code by searching a root directory when they likely want code found elsewhere in the codebase.

`/cmd`

Code for generated binaries. The name of the sub-directory within /cmd should reflect the name of the output binary. It is common to utilize a small `main` function that imports and executes on packages from /internal and / pkg with no other usage.

`/internal`

Private application and package code. This code never gets exported to other applications or packages and is enforced by the Go compiler. You are not limited to the top level `internal` directory. You can have more than one `internal` directory at any level in the codebase tree.

`/pkg`

Public application and package code. This code may be imported by external packages or applications. Since other applications can import code from this directory it is important to ensure proper API contracts are in place as modification of code here could have unwanted downstream effects to other applications or packages.

`/vendor`

Application dependencies. Typically managed manually or by a dependency management tool such as go mod.
Using `go mod vendor` will generate a `/vendor` directory automatically in Go 1.14+.

`/api`

Specifications for APIs such as OpenAPI/Swagger specifications, JSON schema files, Protobuffs definition files, etc.

`/web`

Web application specific components such as static web assets, server side templates, and single-page application templates.

`/config`

Configuration file templates and default configs. Example: confd or consul- template files.

`/init`

System init scripts and process manager configs for services such as systemd, upstart, sysv, runit, etc.

`/script`

Scripts to perform builds, install, analysis, tests, etc. This serves to maintain a terse and clean root Makefile.

`/build`

Assets required for packaging and continuous integration. Packer AMI definitions, Dockerfile, deb/rpm/pkg scripts live in `/build/package`. Continuous Integration scripts live in `/build/ci`.

`/deploy`

Orchestration configurations and templates such as docker-compose, Helm charts, Terraform definitions, etc.

`/doc`

Design and user documentation. Can also include `godoc` generated documentation. Architecture Design Records (ADRs) live in `/doc/arch`.

`/third_party`

External helper tools, forked code, and other third-party utilities such as Swagger UI.

`/githooks`

Git hooks.

## Directories to Avoid

`/src`

Some Go applications incorrectly utilize a `src` folder. This serves to confuse the engineer from the `src` directory found in the $GOROOT path. Utilizing a `src` folder within a Go codebase is a common Java-ism and not accepted in the Go ecosystem.
