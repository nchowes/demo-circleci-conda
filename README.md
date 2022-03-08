
# PYTHON APPLICATION
This Python application repo was created to showcase the integration between GitHub and CircleCI.  
[![CircleCI](https://circleci.com/gh/nchowes/demo-circleci-conda.svg?style=svg)](https://circleci.com/gh/nchowes/demo-circleci-conda)

The configuration follows the steps outlined in a [cicleci blog post](https://circleci.com/blog/setting-up-continuous-integration-with-github/) with modifications for conda environments versus venv. The setup relies on a `config.yml` and a description of this file can be found [here](https://circleci.com/docs/2.0/language-python/). Compare this file with the blog post to see example modifications. 

The docker image specified in the configuration can be found [here](https://hub.docker.com/r/continuumio/miniconda3). The CI builds on a ubuntu linux os. If you are exporting conda dependencies from a different platform, you'll probably deal with cross-platform dependency issues, which will either require specific options to be set when exporting the environment [see resolution](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html), or manual edits to the `environment.yml` file and/or modify the options. For example, using macOS and building on linux (results might be different depending on conda version):   
+ `conda env export > environment.yml` - fails on environment creation with an extensive list of  `ResolvePackageNotFound` due to build specifications. 
+ `conda env export --no-builds > environment.yml` - fails on `libcxx=XX.X.X` 
+ `conda env export --from-history` - passes build