# strawberryfields source map: Analysis and Output

Use this map after `doc_map.md` when output behavior needs function-level verification.

## Fast source navigation
- `rg -n "class Result|def samples|def samples_dict|def state" strawberryfields/result.py`
- `rg -n "samples_expectation|samples_variance|all_fock_probs_pnr" strawberryfields/utils/post_processing.py`
- `rg -n "plot_wigner|plot_fock|plot_quad|generate_" strawberryfields/plot.py`
- `rg -n "gbs_runtime|gbs_sample_runtime" strawberryfields/utils/gbs_analysis.py`
- `rg -n "def graph|def subgraph|def points|def spectrum" strawberryfields/apps/plot.py`

## Source entry points (function-level)
- `strawberryfields/result.py` | `Result.samples`, `Result.samples_dict`, `Result.state` | canonical result-access behavior
- `strawberryfields/utils/post_processing.py` | `samples_expectation`, `samples_variance`, `all_fock_probs_pnr` | statistical post-processing behavior
- `strawberryfields/plot.py` | `plot_wigner`, `generate_wigner_chart`, `plot_fock`, `plot_quad` | plotting behavior and chart payload generation
- `strawberryfields/utils/gbs_analysis.py` | `gbs_runtime`, `gbs_sample_runtime` | runtime estimates for GBS analysis
- `strawberryfields/apps/plot.py` | `graph`, `subgraph`, `points`, `spectrum` | apps-level visual analysis utilities
- `tests/frontend/test_post_processing.py` | post-processing tests | numerical regression checks
- `tests/frontend/test_sf_plot.py` | plotting tests | plotting output contract checks
- `tests/apps/test_plot.py` | apps plotting tests | graph/points/spectrum behavior checks
