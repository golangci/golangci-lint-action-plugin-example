# Golangci-lint-action and Plugins Example

This repository is an example to explain how to use [custom linters](https://golangci-lint.run/contributing/new-linters/#how-to-add-a-private-linter-to-golangci-lint) (plugins) with the [GitHub Action of golangci-lint](https://github.com/golangci/golangci-lint-action).

## Build and Install Plugins

```yml
      - name: Build and install plugins
        run: |
          git clone https://github.com/golangci/example-plugin-linter.git
          cd example-plugin-linter
          go build -o '${{ github.workspace }}/.plugins/example.so' -buildmode=plugin plugin/example.go
        working-directory: ${{ runner.temp }}
        env:
          CGO_ENABLED: 1
```

## Install and Run golangci-lint

```yml
      - name: golangci-lint
        uses: golangci/golangci-lint-action@v3
        with:
          version: v1.53.2
          # The installation mode `goinstall` always uses `CGO_ENABLED=1`.
          install-mode: goinstall
          args: --timeout=5m
```

## Full Example

The [Workflow](https://github.com/golangci/golangci-lint-action-example/blob/main/.github/workflows/basic.yml).
