# forex-clock Technical Notes

## Makefile usage

- `make build` - Builds binary
- `make docs` - Generats API documentation. Generated at `docs/api-output.html`. Open via browser.
- `make get` - Gathers external packages.
- `make release` - Triggers release of version
- `make run` - Runs application by existing built binary.

## Endpoints

API endpoints (methods and request / responses) are defined as part of an [API Blueprint](https://apiblueprint.org/) document at [/docs/api.apib](https://github.com/deezone/forex-clock/blob/master/docs/api.apib). To view, generate the documentation and visit `docs/api-output.html` in a browser.

### Generating API docs

To generate API docs:

```
make docs
```

which is based on the `docs/api.apib` file. Output can be viewed by opening `docs/api-output.html` in a browser.

## Setup

### Configuration using `github.com/marksost/configurator`

See https://github.com/marksost/configurator for an explination of how configuration values are determined based on the priority of the source:
- default values

Example: `Username string `json:"username" env:"DB_USERNAME" default:"forex-clock"` where the default `DB_USERNAME` value is "forex-clock"
- JSON configuration file

> Configuration files like this are not normally used in non-development environments, but are a convenient way to develop locally without having to set a ton of environment variables.

- environment variables
- command-line flag

## Testing

Tests for the application are written with [Ginkgo](http://onsi.github.io/ginkgo/) and [Gomega](http://onsi.github.io/gomega/) to allow for BDD-style testing.

To run the tests locally, first install Ginkgo and Gomega:

```bash
go get -u github.com/onsi/ginkgo/ginkgo
go get -u github.com/onsi/gomega
```

NOTE: Make sure `$GOPATH/bin` is within your terminal's `$PATH`. To check that install ran successfully, run:

```bash
$ which ginkgo
/Users/developer/src/go/bin/ginkgo
```

and ensure a path similar to the above is output. It's important to note that while your output may vary slightly, any output means that your pathing is set up correctly.

And those two utilities are installed, you can run tests with the command:

```bash
ginkgo -r --randomizeAllSpecs --randomizeSuites --failOnPending --cover --trace --race
```

or simply (from within the `go` directory):

```bash
go test
```

NOTE: The latter will skip a fair amount of the Ginkgo built-in functionality, so it's recommended to run the Ginkgo command instead of the standard go version.

Alternatively, you can run a Makefile routine called `test` within this repo, which will install Ginkgo and Gomega and run the tests for you.

For code coverage reports for a specific package, `cd` into a package's directory and run:

```bash
go test -coverprofile=coverage.out
go tool cover -html=coverage.out
```

Alias:

```bash
# "go test with coverage"
alias gotwc='go test -coverprofile=coverage.out && go tool cover -html=coverage.out && rm coverage.out'
```
