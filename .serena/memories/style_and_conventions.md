Code style & conventions:
- Python type hints used in many method signatures; dataclass used for FileReport.
- Docstrings present and concise; functions have clear responsibilities.
- Naming: snake_case for functions/variables; PascalCase for classes; constants in ALL_CAPS.
- Errors/warnings routed via output_handlers dict with keys: info, warning, error; avoid direct prints except fallback and CLI UI.
- Token counting via utils.count_tokens; sample-based estimation for large texts in RepoMap.token_count.
- Paths normalized with pathlib.Path.resolve(); get_rel_fname returns path relative to provided root.
- Caching: diskcache for persistent tags cache .repomap.tags.cache.v1 relative to CWD; in-memory dicts for tree and map caches.
- Tree-sitter queries loaded from queries/(tree-sitter-language-pack|tree-sitter-languages)/*-tags.scm via scm.get_scm_fname.
- Graph/ranking via networkx pagerank; personalization boosts chat files.
- Rendering contexts via grep_ast.TreeContext with color=False; fallback to simple line listings.
- Returns from RepoMap methods are deterministic and use Optional types; report aggregation via FileReport.

Lint/formatting expectations:
- No explicit config files present (.flake8, black, ruff). Use standard PEP8 with black (recommended) and ruff if desired.
- Python 3.13 compatible.

Testing:
- No tests present; manual verification via CLI or MCP tools.

Docstrings and types:
- Prefer explicit typing and short docstrings. Keep public methods documented (already followed in repo).
