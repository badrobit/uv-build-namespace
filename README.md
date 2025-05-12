# uv-build-namespace
demo for namespace build issue

The `uv` build backend system does not seem to respect or be namespace aware.

To replicate issue: 
1. run `uv sync --upgrade` 
2. run `uv build --all --wheel` 

for separate non-propagation run the following: 
1. `uv sync --upgrade` 
2. `uv tree --package fake_service` 
3. observe that `pytest` is not listed as a package dependency for the `fake_service` package