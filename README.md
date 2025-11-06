# ⚙️ MLOps Handbook

[![Powered by Kedro](https://img.shields.io/badge/powered_by-kedro-ffc900?logo=kedro)](https://kedro.org)

**A hands-on guide on the best MLOps practices.**

## 🧩 Overview

The goal of this repo is to provide you with the essentials of MLOps to make reliable and robust Machine Learning workflows.

What you will progressively learn:
1. Analyze you data using EDA tools.
2. Validate the parameters of your pipelines and the dataset you use to train your model.
3. Run Bayesian optimization to find the best hyperparameters.


## 🚀 Quick setup

```bash
# Clone the repository
git https://github.com/YOUR_USERNAME/mlops-handbook.git

cd mlops-handbook
```

After forking the repository, create a new branch to work on your solutions:

```bash
# Create your branch
git checkout -b your-branch-name
```

```mermaid
gitGraph
    commit
    commit
    commit
    branch your-branch-name
    commit id: "your first commit"
```

## 🛠️ Installation

We use **[`uv`](https://github.com/astral-sh/uv)** for the Python environment creation.

You can use uv directly to create your environment and install the dependendcies:
```bash
# Create environment
uv venv
# Install dependencies
uv sync
```

Or you can create a venv and install the dependencies (example using Visual Studio Code):
1. Download the python extension.
2. ```ctrl+shift+p``` or ```cmd+shilf+p``` to open the dropdown menu of the python extensionand select the option to create a python environment `Python: Create Environment...`.
3. Select `venv` (not the quick create).
4. Use the right python version (>=3.12 is recommended).
5. Don't install the dependencies of the project.
6. Once created, you can open the terminal and install the dependencies:
```bash
# Install uv
pip install uv
# Install dependencies
uv sync
```

> 📦 All dependencies are defined in the `pyproject.toml` file.


```bash
# Activate the environment
source .venv/bin/activate  # (on Windows: .venv\Scripts\activate)
```


## 👥 Authors

| [<img src="assets/authors/benjamin.jpeg" width="100" height="100" style="border-radius:50%;">](https://www.linkedin.com/in/benjamin-wallyn/) | [<img src="assets/authors/juan.jpeg" width="100" height="100" style="border-radius:50%;">](https://www.linkedin.com/in/juanpablousuga/) |
|:--:|:--:|
| [**Benjamin Wallyn**](https://www.linkedin.com/in/benjamin-wallyn/) | [**Juan Pablo Usuga Cadavid**](https://www.linkedin.com/in/jpusugacadavid/)|


## Kedro

### Overview

This is your new Kedro project, which was generated using `kedro 1.0.0`.

Take a look at the [Kedro documentation](https://docs.kedro.org) to get started.

### Rules and guidelines

In order to get the best out of the template:

* Don't remove any lines from the `.gitignore` file we provide
* Make sure your results can be reproduced by following a data engineering convention
* Don't commit data to your repository
* Don't commit any credentials or your local configuration to your repository. Keep all your credentials and local configuration in `conf/local/`

### How to install dependencies

Declare any dependencies in `requirements.txt` for `pip` installation.

To install them, run:

```
pip install -r requirements.txt
```

### How to run your Kedro pipeline

You can run your Kedro project with:

```
kedro run
```

### How to test your Kedro project

Have a look at the file `tests/test_run.py` for instructions on how to write your tests. You can run your tests as follows:

```
pytest
```

You can configure the coverage threshold in your project's `pyproject.toml` file under the `[tool.coverage.report]` section.


### Project dependencies

To see and update the dependency requirements for your project use `requirements.txt`. You can install the project requirements with `pip install -r requirements.txt`.

[Further information about project dependencies](https://docs.kedro.org/en/stable/kedro_project_setup/dependencies.html#project-specific-dependencies)

### How to work with Kedro and notebooks

> Note: Using `kedro jupyter` or `kedro ipython` to run your notebook provides these variables in scope: `context`, 'session', `catalog`, and `pipelines`.
>
> Jupyter, JupyterLab, and IPython are already included in the project requirements by default, so once you have run `pip install -r requirements.txt` you will not need to take any extra steps before you use them.

#### Jupyter
To use Jupyter notebooks in your Kedro project, you need to install Jupyter:

```
pip install jupyter
```

After installing Jupyter, you can start a local notebook server:

```
kedro jupyter notebook
```

#### JupyterLab
To use JupyterLab, you need to install it:

```
pip install jupyterlab
```

You can also start JupyterLab:

```
kedro jupyter lab
```

#### IPython
And if you want to run an IPython session:

```
kedro ipython
```

#### How to ignore notebook output cells in `git`
To automatically strip out all output cell contents before committing to `git`, you can use tools like [`nbstripout`](https://github.com/kynan/nbstripout). For example, you can add a hook in `.git/config` with `nbstripout --install`. This will run `nbstripout` before anything is committed to `git`.

> *Note:* Your output cells will be retained locally.

### Package your Kedro project

[Further information about building project documentation and packaging your project](https://docs.kedro.org/en/stable/tutorial/package_a_project.html)
