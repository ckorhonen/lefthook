# Lefthook

## Map and tools

`main.go` and `cmd/` expose the CLI. `internal/config/`, `internal/git/`, and `internal/run/` own configuration, repository interaction, and hook execution; `tests/integration/` exercises complete Git workflows. `gen/` generates schemas, `docs/mdbook/` documents behavior, and `packaging/` handles distributions.

Use Go 1.25.0 as declared in `go.mod`/`CONTRIBUTING.md`; `go mod download` resolves dependencies. `make build` writes the local `lefthook` binary, and `./lefthook --help` checks CLI startup. Preserve cross-platform quoting, exit status, environment handling, and configuration compatibility.

## Checks and effects

Use focused `go test` packages while iterating and `make test` for the defined race-enabled suite (requires a working C toolchain). CI also tests Linux, macOS, and Windows. With golangci-lint 2.7.1 installed, `golangci-lint run` matches the non-fixing lint gate. `make lint` instead downloads the linter if absent and runs `--fix`; inspect its edits.

`make test-integration` depends on `install`, which replaces the binary in GOPATH/bin, then runs integration tests. Use a disposable GOPATH/test repository so validation doesn't replace a user's installed tool or install hooks into their working repo. `make jsonschema` rewrites both schema copies; edit the generator/configuration source and validate regenerated output together. Keep version, packaging, release, and hook-install operations separate from ordinary validation and within their existing authorization.

## Finishing work

Follow the nearby implementation and keep changes within the requested scope. Carry authorized changes through the relevant checks, fixing failures caused by the change. For a bug, reproduce the affected behavior and add a focused regression check when useful. Make routine reversible choices without another approval; ask only when missing information materially changes correctness, scope, or authorization, and name the exact source of any blocking rule. Report what changed, checks actually run, and concrete unverified behavior; repeat checks when new edits or evidence warrant it.
