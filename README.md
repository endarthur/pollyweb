
# Pollyweb: JupyterLite Deployment for Pollywog

This project provides a JupyterLite deployment for running [Pollywog](https://github.com/endarthur/pollywog) directly in your browser—no local Python installation required.

## What is Pollywog?
[Pollywog](https://github.com/endarthur/pollywog) is an open-source Python package for automating workflows involving `.lfcalc` files used in Leapfrog software by Seequent. It enables:

- Programmatic reading and writing of `.lfcalc` files
- Automation of complex workflows (conditional logic, domain-based dilution, post-processing)
- Integration with scikit-learn models for direct use in Leapfrog calculations
- Powerful querying/filtering of calculation sets

See the [Pollywog documentation](https://pollywog.readthedocs.io/en/latest/) for more details and tutorials.

## About This Deployment
This JupyterLite deployment lets you:

- Run Pollywog in your browser, instantly—no Python installation needed
- Explore example notebooks demonstrating Pollywog features
- Prototype and automate Leapfrog workflows interactively

## Getting Started
1. Open the JupyterLite interface (see deployment instructions or launch link)
2. Browse the `content/examples/` folder for ready-to-run notebooks:
	- `quickstart.ipynb`: Quick introduction with installation
	- `basic_usage.ipynb`: Getting started with Pollywog
	- `display_final_workflow.ipynb`: End-to-end workflow example
	- `sklearn_conversion.ipynb`: Integrate scikit-learn models
	- `querying_calcsets.ipynb`: Advanced querying
	- ...and more
3. **Install Pollywog in your notebook** (required for JupyterLite):
   ```python
   # Install pollywog in JupyterLite (skip in regular Jupyter)
   import sys

   if 'pyodide' in sys.modules:
       # Running in JupyterLite/Pyodide - install from bundled wheel
       import micropip
       await micropip.install('lf_pollywog')
       print("✓ Installed pollywog from bundled wheel")
   else:
       # Running in regular Jupyter - assume already installed
       print("✓ Using system-installed pollywog")
   ```
4. Create your own notebooks to automate `.lfcalc` workflows

## Example: Reading and Writing `.lfcalc` Files
```python
import pollywog as pw
calcset = pw.CalcSet.read_lfcalc("path/to/file.lfcalc")
calcset.to_lfcalc("output.lfcalc")
```

## Example: Converting a scikit-learn Model
```python
from pollywog.conversion.sklearn import convert_tree
from sklearn.tree import DecisionTreeRegressor
import numpy as np
X = np.array([[0.2, 1.0, 10], [0.5, 2.0, 20]])
y = np.array([0.7, 0.8])
feature_names = ["Cu_final", "Au_final", "Ag_final"]
reg = DecisionTreeRegressor(max_depth=2)
reg.fit(X, y)
recovery_calc = convert_tree(reg, feature_names, "recovery_ml")
pw.CalcSet([recovery_calc]).to_lfcalc("recovery_ml.lfcalc")
```

## Documentation & Resources
- [Pollywog GitHub](https://github.com/endarthur/pollywog)
- [Pollywog Documentation](https://pollywog.readthedocs.io/en/latest/)
- [Leapfrog Software](https://www.seequent.com/products-solutions/leapfrog/)

## License
MIT License

## Legal Disclaimer
Pollywog is an independent open-source tool and is not affiliated with, endorsed by, or sponsored by Seequent or any company associated with Leapfrog. Use of this tool does not violate Leapfrog’s license terms or Seequent’s policies. See the [Pollywog repository](https://github.com/endarthur/pollywog) for full legal details.


