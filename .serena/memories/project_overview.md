Project: RepoMapper

Purpose:
- Generate a compact, token-bounded “repository map” that highlights important files and the most relevant code definitions, mainly for LLM consumption.
- Works as both a CLI tool and an MCP server.

How it works (high level):
- Discovers files (or uses provided lists).
- Parses source using Tree-sitter via grep-ast to extract definitions and references.
- Builds a graph and ranks files/definitions with PageRank (networkx).
- Selects and formats the highest value lines with TreeContext into a readable map, sized by token budget (tiktoken).
- Caches tags (diskcache) and uses in-memory map caching.

Tech stack:
- Python 3.13+
- Core libs: grep-ast (Tree-sitter), networkx (PageRank), diskcache, tiktoken, pygments
- MCP server: fastmcp

Key modules:
- repomap.py: CLI entry.
- repomap_server.py: MCP stdio server exposing tools repo_map and search_identifiers.
- repomap_class.py: Main RepoMap implementation (parsing, ranking, rendering, caching).
- utils.py: token counting and file reading helpers.
- importance.py: important-file heuristic.
- scm.py: resolves tree-sitter query (SCM) filenames.
- queries/: tree-sitter query files for many languages.

Entrypoints:
- CLI: python repomap.py [options]
- MCP server: python repomap_server.py (stdio)

Notable behavior/flags:
- --chat-files have highest priority; --mentioned-files/--mentioned-idents boost importance; other files provide context.
- --map-tokens controls output size (token budget). --exclude-unranked can hide PR=0 files. --force-refresh clears caches.
- RepoMap.get_repo_map returns (map_string | None, FileReport) in the class.

Supported languages:
- Many with tree-sitter grammars (Python, JS/TS, Java, Go, Rust, C/C++, etc.). See queries/.

License: Apache-2.0