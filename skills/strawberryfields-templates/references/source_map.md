# strawberryfields source map: Templates

Use this map after `doc_map.md` when docs rendering issues require function-level verification.

## Fast source navigation
- `rg -n "autosummary" doc/_templates/autosummary*/*.rst`
- `rg -n "def (get_github_url|html_page_context|setup)" doc/_ext/edit_on_github.py`
- `rg -n "class BaseBackend|class Program|class Result|class Engine" strawberryfields/backends/base.py strawberryfields/program.py strawberryfields/result.py strawberryfields/engine.py`

## Source entry points (function-level)
- `doc/_templates/autosummary_core/module.rst` | core module page rendering template
- `doc/_templates/autosummary_core/class.rst` | core class page rendering template
- `doc/_templates/autosummary/module.rst` | autosummary module listing template
- `doc/_templates/autosummary/class.rst` | autosummary class rendering template
- `doc/_ext/edit_on_github.py` | `get_github_url`, `html_page_context`, `setup` | Sphinx page-context extension behavior
- `doc/conf.py` | Sphinx extension configuration and build options
- `strawberryfields/program.py` | `Program` docstring/API surface used by autodoc
- `strawberryfields/engine.py` | `Engine`/`LocalEngine` docstring/API surface used by autodoc
- `strawberryfields/result.py` | `Result` API surface used by autodoc
- `strawberryfields/backends/base.py` | backend base-class API surface used by autodoc
