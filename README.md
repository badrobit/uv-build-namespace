# uv-build-namespace
demo for namespace build issue

The `uv` build backend system does not seem to respect or be namespace aware.

To replicate issue run the following: 
1. `uv sync --upgrade` 
2. `uv build --all --wheel` 
3. `uv pip install dist/dist/fake_service-0.1.0-py3-none-any.whl`
4. `uv run python -c "import matsbrain.fake_library"` 

It should complain about not being able to find the `fake_library` module.

```shell
$ uv run python -c "import matsbrain.fake_library"

> Traceback (most recent call last):
>   File "<string>", line 1, in <module>
>    import matsbrain.fake_library
> ModuleNotFoundError: No module named 'matsbrain'
```

for separate non-propagation run the following: 
1. `uv sync --upgrade` 
2. `uv tree --package fake_service` 
3. observe that `pytest` is not listed as a package dependency for the `fake_service` package