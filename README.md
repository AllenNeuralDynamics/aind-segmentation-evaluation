# aind-segmentation-evaluation

[![License](https://img.shields.io/badge/license-MIT-brightgreen)](LICENSE)
![Code Style](https://img.shields.io/badge/code%20style-black-black)

[![semantic-release: angular](https://img.shields.io/badge/semantic--release-angular-e10079?logo=semantic-release)](https://github.com/semantic-release/semantic-release)

Python package for performing a skeleton-based evaluation of a predicted segmentation of neural arbors. This tool detects topological mistakes (i.e. splits and merges) in the predicted segmentation by comparing it to the ground truth skeleton. Once this comparison is complete, several statistics (e.g. edge accuracy, split count, merge count) are computed and returned in a dictionary. There is also an optional to write either tiff or swc files that highlight each topological mistake.


## Usage

Here is a simple example of evaluating a predicted segmentation. Note that this package supports a number of different input types, see documentation for details. 

```python
from aind_segmentation_evaluation.run_evaluation import run_evaluation

# Initializations
shape = (148, 226, 282)
data_dir = "./resources"
path_to_pred_volume = os.path.join(data_dir, "pred_volume.tif")
path_to_target_volume = os.path.join(data_dir, "target_volume.tif")
target_graphs_dir = os.path.join(data_dir, "target_graphs")

# Evaluation
stats = run_evaluation(
        shape,
        target_graphs_dir=target_graphs_dir,
        path_to_pred_volume=path_to_pred_volume,
        output="tif",
        output_dir=data_dir,
    )

# Report results
print("Graph-based evaluation...")
for key in stats.keys():
    print("   " + key + ":", stats[key])
```

## Installation
To use the software, in the root directory, run
```bash
pip install -e .
```

To develop the code, run
```bash
pip install -e .[dev]
```

To install this package from PyPI, run
```bash
pip install aind-segmentation-evaluation
```

### Pull requests

For internal members, please create a branch. For external members, please fork the repository and open a pull request from the fork. We'll primarily use [Angular](https://github.com/angular/angular/blob/main/CONTRIBUTING.md#commit) style for commit messages. Roughly, they should follow the pattern:
```text
<type>(<scope>): <short summary>
```

where scope (optional) describes the packages affected by the code changes and type (mandatory) is one of:

- **build**: Changes that affect build tools or external dependencies (example scopes: pyproject.toml, setup.py)
- **ci**: Changes to our CI configuration files and scripts (examples: .github/workflows/ci.yml)
- **docs**: Documentation only changes
- **feat**: A new feature
- **fix**: A bugfix
- **perf**: A code change that improves performance
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **test**: Adding missing tests or correcting existing tests
