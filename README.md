# Simpler cookiecutter
This is my version of the [Cookiecutter Data Science project](https://drivendata.github.io/cookiecutter-data-science/). I initially started using that project, but got confused and tangle with a lot of concepts I do not know. I couldn't find a step-by-step example using that project, so I decided to take a step back, and lay a project structure that makes sense to me and my work methodology. I suspect the complications I didn't unerstand from the original project are in part due to my inexperience, and in part due to the project's intention to cater to a broad audience, which adds overhead complexity, unecessary for the uninitiated (🙋‍♂️).


# Start here: Things you will want to change
There are a few changes we need to apply to adapt this template to a new project. Once you have downloaded or cloned this repo please follow these steps: 

## Project name
Change the name of the project directory folder to a name that makes sense with your project:
1. Project directory name: current name is simplified_project_cookiecutter

## Conda environment name
This template assumes you are using conda for managing environmnets. The environment name is defined in a few places that you'll need to modify (they should all have the same value):

2. `environment.yml`: Current environment name is set with `name: my_env_name`

3. `tasks.py`: Current environment name is set with `ENV_NAME = 'my_env_name'`

4. `Makefile`: Current environment name is set with `PROJECT_NAME = my_env_name`

## Package name
By default we create a Python package named `src` by defining the `setup.py` and by adding it as a dependency to the `environment.yml file`. If you would like your package to have a different name you can change the file:

5. `setup.py`: Current package name is set with `name='src'`

## Author name
The author name appears in a couple of places:

1. `setup.py`: Currently set with `author='Rafael Pinto'`
2. `LICENSE`: Currently on the third line. You might want to choose a different [license for your project](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/licensing-a-repository)


# Set conda environment
After tailoring the environment and project names with the instructions above we are ready to start working the project. First we will set up the conda environment. Then we will see how to use invoke to update our environment.

## Check the initial dependencies
Check that the `environment.yml` file has the regular libraries that you will need to start a project. I've added a few that I find useful, but you can add or remove as you please. My current workflow uses invoke, papermill, and python-dotenv, so if you want to follow along you will need those.

## The need for `invoke`
Open the `task.py` file. Here we record a set of useful commands for setting and updating the conda environment. In addition, you will define your workflow's key execution steps on this file. I think of `task.py` as a substitute for the `Makefile`. I was happily using `make` until I had to start developing on Windows.

`make` comes preloaded in almost all OS X systems, but not on Windows. Installing it on Windows is not a trivial task, specially without elevated privileges. Therefore, I'll use `invoke`, as it is Python native, and provides similar functionality as what I need from `make`. The latter is still on this template if you prefer that. Just pick one and stick to it.

## Create and activate conda environment
Now we are ready to create the conda environment. This and the environment activation are the only steps that can't be added as a task to the `tasts.py` file:

> For consistencies use the same environment name that you set on the **Conda environment name** section above. Replace `my_env_name` in the code below with your environment name.

On a terminal window:
```shell
conda env create --name my_env_name --file environment.yml
conda activate my_env_name
```

## Set up Jupyter
With the environment activated we can run our first task for setting up a named jupyter kernel, and for adding notebook extensions (time cell, table of content, word highlighting).

On the project directory run:
```shell
invoke env-set-jupyter
```

> Note that the syntaxt uses kebab-case and not snake_case.

## Freeze environment
We will use a two YAML file strategy for keeing track of dependencies:

1. `environment.yml`: Built by hand for humans. Comes with this template. Keeps a manageble list of dependencies. You will want to add new dependencies here.

2. `environment_to_freeze.yml`: It is built from the current activated environment using `invoke env-to-freeze` (that is `conda env export` behind the scenes) for computers. It is meant to keep a detailed list of your dependencies, and their respective dependencies, so anyone can reproduce your conda environment with `invoke env-update`.

At this point we are ready to create aour first `environment_to_freeze.yml` file:

```shell
invoke env-to-freeze
```

## Add or remove dependencies to your conda environment
Since this is a common task, I added the `invoke env-update` command. Suppose you want to add `scikit-learn`:

1. Add `scikit-learn` to your `environment.yml` file.
2. Update the environment. On a teminal run: `invoke env-update`
3. Freeze the environment. On a teminal run: `invoke env-to-freeze`

Now `scikit-learn` is in both of your YAML files.


# How to operate




