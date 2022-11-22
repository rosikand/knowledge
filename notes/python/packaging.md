---
categories: [advanced, packaging]
---

# Python packaging 

... to be updated. 

## Cool 

- [Poetry](https://python-poetry.org/): basically does all the building work for you. See [here](https://github.com/ikostrikov/jaxrl) for an example. 
- I also think having `setup.py` and installing from GH is the move with github CI actions for auto-version updating. See [here](https://github.com/dibyaghosh/autogit) for minimal example. 


## Poetry tutorial 

### Create 

1. `poetry new package-name`:

```
package-name/
├── package-name/
│   └── __init__.py
├── tests/
│   ├── __init__.py
│   └── test_package-name.py
├── pyproject.toml
└── README.md
```

2. Edit `pyproject.toml` as needed 
3. Run `pipreqs ../` in `package-name/package-name` 
4. Make poetry lock file and auto-specify dependecies via `poetry add $( cat requirements.txt )`
5. Build the dist: `poetry build`
6. (First time) configure PyPI credentials `poetry config pypi-token.pypi my-token` where `my-token` is your api token. 
7. Publish to PyPI: `poetry publish` 
8. (Optional) add `dist/` to a `.gitignore`. 

### Update 

1. (Optional) dependency resolvation: 
   1. Run `pipreqs ../` in `package-name/package-name` 
   2. Make poetry lock file and auto-specify dependecies via `poetry add $( cat requirements.txt )`
2. Edit version number in `pyproject.toml`
3. Build the dist: `poetry build`
4. Publish to PyPI: `poetry publish` 
