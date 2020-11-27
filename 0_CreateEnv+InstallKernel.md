# Create Virtualenv for Jupyter

Mac seems to have Python27 as default Python

Check what version by python --version

You may need to replace python with python38

## install virtualenv

pip install virtualenv

## make virtual environment

python -m venv env20201104

## activate it

source /Users/andrewgaitskell/Code/PythonEnvs/env20201104/bin/activate

## install micropython kernel

Follow install instructions in following link:

https://pypi.org/project/jupyter-micropython-remote/

It is roughly:

pip install jupyter

pip install jupyter_micropython_remote

