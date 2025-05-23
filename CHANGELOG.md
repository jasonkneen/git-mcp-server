# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## v2.0.11 - 2025-05-14

### Fixed

- (logging) Replaced direct `console.log` calls for server startup messages in HTTP and STDIO transports with `logger.notice()` to ensure MCP client compatibility and prevent parsing issues. (Addresses GitHub Issue #9)
- (logging) Refactored internal logger (`utils/internal/logger.ts`):
    - Deferred informational setup messages (e.g., logs directory creation, console logging status) to use the logger's own `info()` method after Winston is initialized.
    - Made critical pre-initialization `console.error` and `console.warn` calls conditional on TTY to prevent non-JSONRPC output when running in stdio mode with an MCP client.
    - Extracted console formatting logic into a reusable helper function (`createWinstonConsoleFormat`) to reduce duplication.
    - Added comments explaining TTY-conditional logging for clarity.

### Changed

- (chore) Updated various dependencies (e.g., `@modelcontextprotocol/sdk`, `@types/node`, `openai`).
- (docs) Refreshed `docs/tree.md` to include `mcp.json` and reflect current structure.

### Other

- Bump version to 2.0.11.

## v2.0.10 - 2025-05-07

### Added

- (dev) Added MCP Inspector configuration (`mcp.json`) to define server settings for `git-mcp-server` and `git-mcp-server-http` when using the inspector. (bf3a164)
- (dev) Added npm scripts `inspector` and `inspector:http` to easily launch the MCP Inspector with the defined configurations. (bf3a164)

### Dependencies

- Added `@modelcontextprotocol/inspector: ^0.11.0` to `dependencies`. (bf3a164)

### Changed

- (docs) Updated version badge in `README.md` to `2.0.10`. (bf3a164)

### Other

- Bump version to 2.0.10. (bf3a164)

## v2.0.9 - 2025-05-07

### Added

- (gitLog) Group commit logs by author in the JSON response, providing a more structured view of commit history. (5b5e037)

### Changed

- (security) Refactored path sanitization (`sanitizePath`) across all tools to use an object response (`SanitizedPathInfo`), improving robustness and providing more context. This includes updated JSDoc, standardized error handling within sanitization, and minor refactors to other sanitization functions. (5b5e037)
- (gitDiff) The 'diff' field in the `gitDiff` tool's response now includes the string "No changes found." directly when no differences are detected, ensuring consistent output format. (5b5e037)

### Other

- Bump version to 2.0.9. (bfe23ea)

## v2.0.8 - 2025-05-07

### Fixed

- Resolved issue where Windows drive letters could be stripped from absolute paths during sanitization when `allowAbsolute` was not explicitly true. This primarily affected `git_set_working_dir` and other tools when absolute paths were provided. The `sanitizePath` calls in git tool logic now correctly pass `{ allowAbsolute: true }`. Fixes GitHub Issue #8. (`6f405a1`)

### Changed

- (security) Update `sanitizePath` calls in all git tool logic to explicitly pass `{ allowAbsolute: true }` ensuring correct handling of absolute paths. (`6f405a1`)

### Dependencies

- Update `@types/node` from `^22.15.9` to `^22.15.15`. (`c28fe86`)

### Other

- Bump version to 2.0.8 (implicitly, as part of user's update process and reflected in package.json by commit `c28fe86` which was intended for 2.0.7 but now aligns with 2.0.8)

## v2.0.5 - 2025-05-05

### Added

- (tools) Enhance `git_commit` tool result to include commit message and committed files list (`1f74915`)

### Changed

- (core) Alphabetize tool imports and initializers in `server.ts` for better organization (`1f74915`)
- (docs) Refine `git_commit` tool description for clarity (`1f74915`)

### Other

- Bump version to 2.0.5 (`1f74915`)

## v2.0.4 - 2025-05-05

- (docs): Added smithery.yaml

## v2.0.3 - 2025-05-05

### Added

- (tools) Enhance git_commit escaping & add showSignature to git_log (`312d431`)

### Changed

- (core) Update server logic and configuration (`75b6683`)
- (tools) Update git tool implementations (`8b9ddaf`)
- (transport) Update transport implementations and add auth middleware (`a043d20`)
- (internal) Consolidate utilities and update types (`051ad9f`)
- Reorganize utilities and server transport handling (`b5c5840`)

### Documentation

- Update project structure in README and tree (`bc8f033`)
- (signing) Improve commit signing docs and add fallback logic (`de28bef`)
- Update README and file tree, remove temporary diff file (`3f86039`)

### Other

- **test**: Test automatic commit signing (commit.gpgsign=true) (`ef094d3`)
- **chore**: Update dependencies (`3cb662a`)
