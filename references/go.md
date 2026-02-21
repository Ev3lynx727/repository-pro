# Go Project Templates

## go.mod

```go
module github.com/username/project

go 1.21

require (
	github.com/stretchr/testify v1.8.4
	github.com/spf13/cobra v1.8.0
)
```

## Makefile

```makefile
.PHONY: build test lint clean install

BINARY_NAME=myapp
VERSION=$(shell git describe --tags --always --dirty)
BUILD_TIME=$(shell date -u '+%Y-%m-%d_%H:%M:%S')

build:
	CGO_ENABLED=0 go build -ldflags="-s -w -X main.version=${VERSION} -X main.buildTime=${BUILD_TIME}" -o bin/${BINARY_NAME} ./cmd/app

test:
	go test -v -race -coverprofile=coverage.out ./...

lint:
	golangci-lint run ./...

fmt:
	go fmt ./...

tidy:
	go mod tidy

clean:
	rm -rf bin/ coverage.out

install:
	go install ./...

run:
	go run ./cmd/app
```

## .golangci.yml

```yaml
run:
  timeout: 5m

linters:
  enable:
    - errcheck
    - gosimple
    - govet
    - ineffassign
    - staticcheck
    - unused
    - gofmt
    - goimports
    - misspell

linters-settings:
  errcheck:
    check-type-assertions: true
  govet:
    enable-all: true
  gofmt:
    simplify: true

issues:
  exclude-use-default: false
  max-issues-per-linter: 0
  max-same-issues: 0
```

## CI Workflow for Go

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Go
        uses: actions/setup-go@v5
        with:
          go-version: '1.21'
          cache: true
      - run: go mod download
      - run: go test -v -race -coverprofile=coverage.out ./...
      - uses: codecov/codecov-action@v4

  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run golangci-lint
        uses: golangci/golangci-lint-action@v4
        with:
          version: latest

  build:
    needs: [test, lint]
    runs-on: ubuntu-latest
    strategy:
      matrix:
        goos: [linux, darwin, windows]
        goarch: [amd64, arm64]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-go@v5
        with:
          go-version: '1.21'
          cache: true
      - name: Build
        env:
          GOOS: ${{ matrix.goos }}
          GOARCH: ${{ matrix.goarch }}
        run: |
          ext=""
          if [ "$GOOS" = "windows" ]; then
            ext=".exe"
          fi
          CGO_ENABLED=0 go build -ldflags="-s -w" -o bin/${GOOS}_${GOARCH}/myapp${ext} ./cmd/app
      - uses: actions/upload-artifact@v4
        with:
          name: binary-${{ matrix.goos }}-${{ matrix.goarch }}
          path: bin/${{ matrix.goos }}_${{ matrix.goarch }}/*
```

## Package Structure

```
my-project/
├── cmd/
│   └── app/
│       ├── main.go
│       └── app.go
├── internal/
│   ├── config/
│   │   └── config.go
│   ├── handler/
│   │   └── handler.go
│   └── middleware/
│       └── middleware.go
├── pkg/
│   └── utils/
│       └── utils.go
├── api/
│   └── openapi.yaml
├── go.mod
├── go.sum
├── Makefile
├── .golangci.yml
└── README.md
```

## Cobra CLI Structure

```go
package main

import (
	"fmt"
	"github.com/spf13/cobra"
)

var rootCmd = &cobra.Command{
	Use:   "myapp",
	Short: "A brief description",
	Long:  `A longer description`,
	Run: func(cmd *cobra.Command, args []string) {
		fmt.Println("Hello, World!")
	},
}

func main() {
	if err := rootCmd.Execute(); err != nil {
		fmt.Fprintln(os.Stderr, err)
		os.Exit(1)
	}
}
```
