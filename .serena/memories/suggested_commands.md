Environment (Windows):
- Ensure Python 3.13+ and a virtual environment.

Setup:
- py -3.13 -m venv .venv
- .venv\Scripts\activate
- pip install -r requirements.txt

Run CLI:
- python repomap.py .
- python repomap.py src/ --map-tokens 2048
- python repomap.py --chat-files main.py --other-files src/
- python repomap.py --mentioned-files config.py --mentioned-idents main_function
- python repomap.py . --verbose --force-refresh --model gpt-4 --max-context-window 8192 --exclude-unranked

Run MCP server (stdio):
- python repomap_server.py

Cline/Roo MCP config snippet (edit path):
- command: C:\\Path\\To\\python.exe
- args: ["C:\\absolute\\path\\to\\repomap_server.py"]

Useful Windows shell commands:
- dir, cd, type file.txt
- findstr /s /i "pattern" *
- python -m pip install <pkg>
- git clone <url> | git status | git add -A | git commit -m "msg" | git push

Notes:
- The tool downloads tree-sitter grammars via grep-ast deps; first run may take time.
- If token_limit invalid in MCP, defaults to 8192.
- Use --force-refresh to invalidate tag caches (.repomap.tags.cache.v1).