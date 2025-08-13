---
description: Repository Information Overview
alwaysApply: true
---

# MCP Toolbox for Databases Information

## Summary

MCP Toolbox for Databases is an open-source MCP server for databases that enables developers to build tools for AI agents to access data in various databases. It handles complexities like connection pooling, authentication, and security, while providing simplified development, better performance, enhanced security, and end-to-end observability.

## Structure

- **cmd/**: Command-line interface implementation
- **internal/**: Core implementation components
  - **auth/**: Authentication mechanisms
  - **log/**: Logging functionality
  - **prebuiltconfigs/**: Pre-configured tool definitions
  - **server/**: Server implementation
  - **sources/**: Database source implementations
  - **telemetry/**: Observability and metrics
  - **tools/**: Tool implementations for various databases
  - **util/**: Utility functions
- **tests/**: Integration tests for all supported databases
- **docs/**: Documentation files
- **.ci/**: Continuous integration configuration
- **.github/**: GitHub workflows and templates

## Language & Runtime

**Language**: Go
**Version**: Go 1.24 (toolchain go1.24.5)
**Build System**: Go modules
**Package Manager**: Go modules

## Dependencies

**Main Dependencies**:

- Cloud database clients (AlloyDB, BigQuery, Bigtable, Spanner, Firestore)
- Database drivers (MySQL, PostgreSQL, MongoDB, Redis, Neo4j)
- HTTP frameworks (chi)
- Configuration (go-yaml)
- CLI (cobra)
- Telemetry (OpenTelemetry)

**Development Dependencies**:

- Testing frameworks (standard Go testing)
- Linting (golangci-lint)

## Build & Installation

```bash
# Install from source
go install github.com/googleapis/genai-toolbox@latest

# Build locally
go build -o toolbox

# Run the server
./toolbox --tools-file "tools.yaml"
```

## Docker

**Dockerfile**: Dockerfile
**Base Image**: gcr.io/distroless/static:nonroot
**Build Command**:

```bash
docker build -t toolbox:dev .
docker run -d toolbox:dev
```

## Testing

**Framework**: Go testing package
**Test Location**:

- Unit tests: Alongside implementation files
- Integration tests: tests/ directory

**Test Command**:

```bash
# Run unit tests
go test -race -v ./...

# Run integration tests for specific database
go test -race -v ./tests/<DATABASE_DIR>

# Run with coverage
go test -c -race -cover -coverpkg=./internal/sources/...,./internal/tools/... ./tests/...
```

## Main Entry Points

**Main File**: main.go
**Command Structure**: cmd/root.go
**Server Implementation**: internal/server/server.go
**Configuration**: tools.yaml (user-provided)

## Tooling & SDKs

The project provides client SDKs for various languages and frameworks:

- Python: Core, LangChain, LlamaIndex
- JavaScript/TypeScript: Core, LangChain, Genkit
- Go: Core SDK

## Deployment Options

- Binary installation
- Container deployment
- Homebrew installation (macOS/Linux)
- Compilation from source
