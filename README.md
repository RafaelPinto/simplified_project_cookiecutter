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


# How to operate




