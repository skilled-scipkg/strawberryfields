# strawberryfields source map: Advanced Topics

Use this map after `doc_map.md` when metadata answers need code-level verification.

## Fast source navigation
- `rg -n "def (version|about|cite)|__version__" strawberryfields/__init__.py strawberryfields/_version.py`
- `rg -n "class Device|def validate_|def create_program" strawberryfields/device.py`
- `rg -n "from_blackbird|to_blackbird|from_xir|to_xir" strawberryfields/io`

## Source entry points (function-level)
- `strawberryfields/__init__.py` | `version`, `about`, `cite` | package metadata and citation behavior
- `strawberryfields/_version.py` | `__version__` | canonical version string
- `strawberryfields/device.py` | `Device.validate_target`, `Device.validate_parameters`, `Device.create_program` | device metadata constraints
- `strawberryfields/io/blackbird_io.py` | `from_blackbird`, `to_blackbird` | Blackbird conversion reference behavior
- `strawberryfields/io/xir_io.py` | `from_xir`, `to_xir` | XIR conversion reference behavior
- `tests/frontend/test_about.py` | `test_about` | validates `sf.about()` output contract
- `tests/api/test_devicespec.py` | device spec tests | validates device parameter checks
- `tests/frontend/io/test_io_blackbird.py` | IO tests | validates Blackbird conversion behavior
