# Harness Open Source

Harness is an open source DevOps platform that brings together code hosting, automated pipelines, hosted development environments (Gitspaces) and artifact registries.

## Features
- Git repository management
- Continuous integration pipelines
- Hosted developer environments
- Artifact registry

## Getting Started
### Run with Docker
```bash
docker run -d \
  -p 3000:3000 \
  -p 22:22 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /tmp/harness:/data \
  --name harness \
  --restart always \
  harness/harness
```
Open `http://localhost:3000` once the container is running.

### Build from Source
Install Go 1.20 or newer and a recent Node version, then run:
```bash
make dep
make tools
pushd web && yarn install && yarn build && popd
make build
```
Start the server with:
```bash
./gitness server .local.env
```

### Update the UI Client
After changing REST APIs:
1. `./gitness swagger > web/src/services/code/swagger.yaml`
2. `cd web && yarn services`

### Tests
Run all Go tests:
```bash
make test
```

### Registry Conformance Tests
```bash
make conformance-test
```
To test against a running server:
```bash
make hot-conformance-test
```

### What about Drone?
Drone lives on in the [`drone` branch](https://github.com/harness/harness/tree/drone). Harness expands on Drone, and aims to achieve full pipeline compatibility in the future.

## CLI
After building, `./gitness --help` lists the available commands.

## Contributing
See [CONTRIBUTING.md](CONTRIBUTING.md).

## Documentation
Visit [developer.harness.io](https://developer.harness.io/docs/open-source) for guides and additional information.

## License
Harness is licensed under the Apache License 2.0. See [LICENSE](LICENSE).
