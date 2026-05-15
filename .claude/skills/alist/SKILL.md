```markdown
# alist Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you how to contribute to the `alist` project, a Go-based codebase for storage and indexing solutions. You'll learn the project's coding conventions, common workflows (such as adding drivers, updating dependencies, and refactoring), and how to use suggested commands to streamline your contributions. This guide is based on repository analysis and reflects real-world development patterns in `alist`.

## Coding Conventions

**File Naming**
- Use `camelCase` for file names.
  - Example: `searchNode.go`, `metaData.go`

**Import Style**
- Use relative imports within the module.
  - Example:
    ```go
    import (
        "internal/db"
        "internal/search"
    )
    ```

**Export Style**
- Use named exports for functions, types, and variables.
  - Example:
    ```go
    // Exported function
    func NewDriver() *Driver {
        // ...
    }
    ```

**Commit Messages**
- Follow [Conventional Commits](https://www.conventionalcommits.org/) with these prefixes: `fix`, `feat`, `chore`, `refactor`.
- Keep commit messages concise (average 54 characters).
  - Example: `feat: add support for new S3 driver`

## Workflows

### Add or Update Driver
**Trigger:** When you want to add support for a new storage provider or update an existing driver's functionality.  
**Command:** `/add-driver`

1. Create or update the driver implementation file:  
   `drivers/<driver>/driver.go`
2. Create or update the driver metadata file:  
   `drivers/<driver>/meta.go`
3. Create or update the types file:  
   `drivers/<driver>/types.go`
4. Create or update utility/helper file:  
   `drivers/<driver>/util.go`
5. Optionally, register the new driver in:  
   `drivers/all.go`

**Example:**
```go
// drivers/mycloud/driver.go
package mycloud

type MyCloudDriver struct { /* ... */ }

func (d *MyCloudDriver) Connect() error { /* ... */ }
```

### Search Index Enhancement
**Trigger:** When you want to improve or add to the search/indexing capabilities.  
**Command:** `/update-search-index`

1. Modify or enhance core search logic:  
   `internal/search/*.go`
2. Update or add database search node logic:  
   `internal/db/searchnode.go`
3. Update or add search models:  
   `internal/model/search.go`
4. Update or add index handlers:  
   `server/handles/index.go`
5. Optionally, update settings or constants:  
   `internal/conf/const.go`, `internal/bootstrap/data/setting.go`
6. Optionally, update server routes:  
   `server/router.go`

**Example:**
```go
// internal/search/search.go
func SearchFiles(query string) ([]File, error) {
    // Enhanced search logic here
}
```

### Dependency Update
**Trigger:** When you want to update third-party dependencies to newer versions.  
**Command:** `/update-deps`

1. Update `go.mod` with new dependency versions.
2. Update `go.sum` to match.
3. Optionally, run `go mod tidy` to clean up unused dependencies.

**Example:**
```sh
go get github.com/new/dependency@latest
go mod tidy
```

### CI Workflow Update
**Trigger:** When you want to change CI/CD automation behavior.  
**Command:** `/update-ci`

1. Modify workflow YAML files in `.github/workflows/`.
2. Optionally, update related scripts or configuration files.

**Example:**
```yaml
# .github/workflows/ci.yml
on:
  push:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Go
        uses: actions/setup-go@v3
        with:
          go-version: 1.20
```

### Refactor Cross-Package
**Trigger:** When you want to reorganize code for better separation of concerns or maintainability.  
**Command:** `/refactor-package`

1. Move or split methods between packages (e.g., `db` → `op`, `fs` → `op`).
2. Update all references and imports.
3. Rename variables, files, or methods for clarity.
4. Update related tests.

**Example:**
```go
// Before: internal/db/file.go
func SaveFile(f File) error { ... }

// After: internal/op/file.go
func SaveFile(f File) error { ... }
```

## Testing Patterns

- Test files use the pattern `*.test.*` (e.g., `driver.test.go`).
- The specific testing framework is not specified, but Go's standard `testing` package is likely.
- Place test files alongside the code they test.

**Example:**
```go
// drivers/mycloud/driver.test.go
package mycloud

import "testing"

func TestConnect(t *testing.T) {
    // Test logic here
}
```

## Commands

| Command             | Purpose                                                     |
|---------------------|-------------------------------------------------------------|
| /add-driver         | Add or update a storage driver implementation               |
| /update-search-index| Enhance or modify search and indexing features              |
| /update-deps        | Update Go module dependencies                              |
| /update-ci          | Update CI/CD GitHub Actions workflows                      |
| /refactor-package   | Refactor logic across multiple packages for maintainability |
```
