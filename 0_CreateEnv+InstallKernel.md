# Create Virtualenv for Jupyter

Mac seems to have Python27 as default Python

Check what version by python --version

You may need to replace python with python38

## install virtualenv

pip install virtualenv

## make virtual environment

python -m venv env20201104

## activate it

/Users/andrewgaitskell/Code/PythonEnvs/env20201104/bin/activate

Follow install instructions in following link:

https://pypi.org/project/jupyter-micropython-remote/

It is roughly:

pip install jupyter

pip install jupyter_micropython_remote

## open up jupyter

jupyter notebook

you should then find the micropython kernel available and you can start with esp8266 notebook

https://github.com/andrewcgaitskell/micro-python/blob/main/3_MQTTESP8266.ipynb

You need the Chrome Plugin to view the above notebook
