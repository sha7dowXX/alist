---
name: add-or-update-driver
description: Workflow command scaffold for add-or-update-driver in alist.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /add-or-update-driver

Use this workflow when working on **add-or-update-driver** in `alist`.

## Goal

Adds a new storage driver or updates an existing one, including implementation, metadata, types, and utility files.

## Common Files

- `drivers/*/driver.go`
- `drivers/*/meta.go`
- `drivers/*/types.go`
- `drivers/*/util.go`
- `drivers/all.go`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Create or update driver implementation file (drivers/<driver>/driver.go)
- Create or update driver meta file (drivers/<driver>/meta.go)
- Create or update types file (drivers/<driver>/types.go)
- Create or update utility/helper file (drivers/<driver>/util.go)
- Optionally, update drivers/all.go to register the new driver

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.