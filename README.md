# RE:BT-Espresso, Representation Exploitation of BT-Espresso for Behavior Trees Learned from Robot Demonstrations 

IMPORTANT: Although this repo may not be the cleanest code, we have tried to make it more readable. This will be cited as "`open-source`" in the sense that all code can be audited/read. I personally find pseudo code within papers more difficult to read than poorly written real code. If you are looking for the algorithm described within the paper, you will want to look at `BehaviorTreeDev/BehaviorTreeBuilder.py` starting with function `re_bt_espresso`. Feel free to contact groechel@usc.edu if you have any questions. Note from Tom: I just finished my Ph.D. and am working in industry/do not currently have bandwidth to support this repo. If someone else would like to own it, feel free! I am happy to answer questions.

`BehaviorTreeBuilder` is split up as the following:
- `BTBuildGlobals.py` -> contains all global variables (mostly dictionary lookups) w/ descriptions
- `BTBuilderData.py` -> contains functions that build global data (typically dictionaries)
- `BTBuilderHelpers.py` -> contains helper functions (e.g., `save_tree`)
- `BTBuilderLAT.py` -> contains functions for the Last Action Taken Sequence/Cycles algorithm (algorithm 2 within the paper)
- `BehaviorTreeBuilder.py` -> contains the RE-BT:Espresso algorithm code using all of the above (algorithm 1 within the paper)

---
## Install
1. Clone repo
2. Install python3 dependencies below (you can create a  python3 [virtual environment](https://docs.python.org/3/library/venv.html) and activate it if you would like first)
3. Fix [pyeda library error](#pyeda-literal-error)

## Running Experiments
In the top level directory, to run all experiments:
`python3 run_experiments.py [-r, --recolor] [-c --config] [-m --multiprocess]`
where `-r` is an optional flag to also re-color the trees, `-c` allows a specification of a single experiment, `-m` flag runs all experiments in parallel, and '-k' runs the original `bt_espresso` algo alongside `re_bt_espresso`. By default, all experiments are run.

Autogenerated usage:
```
usage: run_experiments.py [-h] [-c CONFIG] [-r] [-m] [-k]

optional arguments:
  -h, --help            show this help message and exit
  -c CONFIG, --config CONFIG
                        Name of experiment config json, without this flag it will recurse though all experiments. `expr0.json` as an example.
  -r, --recolor         Run recoloring of all trees
  -m, --multiprocess    Run experiments in ||
  -k, --kevin           Run w original BT-Espresso also
```

## Experiment Pipeline
1. DataSim
2. BuildBT
    * Normalize
    * Hotencode
    * [OPTIONAL] SVMSMOTE Upsampling
    * Learn and Build BT
3. [OPTIONAL] ReColorBT
4. RunResults


## Dependencies

- [Python 3](https://www.python.org/downloads/)
- [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html) 
- [scikit-learn](https://scikit-learn.org/stable/index.html)
- [imblearn](https://imbalanced-learn.readthedocs.io/en/stable/index.html)
- [graphviz](https://graphviz.readthedocs.io/en/stable/index.html)
- [matplotlib](https://matplotlib.org/) 
- [lxml](https://lxml.de/)
- [py_trees](https://py-trees.readthedocs.io/en/devel/)
- [pyeda](https://pypi.org/project/pyeda/)
- [networkx](https://networkx.org/)
- [pydot](https://pypi.org/project/pydot/)

Easy copy paste:
```
pip3 install pandas sklearn graphviz imblearn matplotlib lxml py_trees pyeda networkx
sudo apt-get install graphviz
```

Results analysis `expr_analysis.ipynb` also depends on the following:
- [matplotlib](https://matplotlib.org/)
- [seaborn](https://seaborn.pydata.org/)

Easy copy paste:
```
pip3 install matplotlib seaborn
```

### Pyeda Literal Error
There is a bug is Pyeda library that also need to be fixed. See [#17](https://github.com/interaction-lab/BTFromSARDemostration/issues/17) for fix.



