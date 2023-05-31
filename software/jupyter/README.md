# Changing the Python version Jupyter uses

Sometimes you want to change the version of Python that Jupyter is using! Often this is because you want to make your command-line python command match the version that Jupyter is using.

Jupyter doesn’t use the PATH variable to figure out which Python to use, it uses specific settings called kernels. As a result, if you upgrade or change Pythons on the command line, Jupyter might still be stuck in the past!

## Confirm our Python version
Install the ipykernel package for managing Jupyter settings
Use ipykernel to change our default Jupyter
```
$ python --version
Python 3.10.0
$ python -m pip install ipykernel
$ python -m ipykernel install --user
Installed kernelspec python3 in /Users/soma/Library/Jupyter/kernels/python3
```
This kernel or kernelspec is the settings file that Jupyter uses to figure out what Python it should point to. Now it’s updated, so everything should work great! Shut down your Jupyter notebook server, start a new one, and you’ll be good to go.

When I say “shut down your Jupyter notebook server,” I don’t mean close your notebook tab: that isn’t enough! You need to actually turn off and restart the entire Jupyter server. Use Ctrl+C to shut it down from the command line.

## Double-checking the kernel installed correctly
If we’re nosy or suspicious, we could actually look at the kernel’s details. Read the last line of the output to see where the kernelspec (kernel specification) lives:

```
$ python -m ipykernel install --user
Installed kernelspec python3 in /Users/soma/Library/Jupyter/kernels/python3
```
The settings are stored in a file called kernel.json inside of this folder. To check up on the details, we can use the cat command.
```
$ cat /Users/soma/Library/Jupyter/kernels/python3/kernel.json 
{
 "argv": [
  "/Users/soma/.pyenv/versions/3.10.0/bin/python",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "Python 3 (ipykernel)",
 "language": "python",
 "metadata": {
  "debugger": true
 }
}
```
The important part here is /Users/soma/.pyenv/versions/3.10.0/bin/python - that’s the exact Python file that Jupyter will be running!

# Adding different Pythons versions in Jupyter notebooks

Sometimes you want to completely upgrade the Python that Jupyer uses, but sometimes you think it would be nice to have multiple versions of Python available in Jupyter. It’s pretty easy!

Before we get started, you’ll want to switch to the python that you’re interested in using in Jupyter. This might mean using pyenv shell, changing your virtualenv, or using a full path like /Library/Frameworks/Python.framework/Versions/3.6/bin/python instead of just python.

In these commands, we’re going to go through three steps:

Confirm our Python version
Install the ipykernel package for managing Jupyter settings
Use ipykernel to add a Jupyter kernel with a specific name
```
$ python --version
Python 3.8.2
$ python -m pip install ipykernel
$ python -m ipykernel install --user --name python3.8.2 --display-name "Python 3.8.2" 
Installed kernelspec python3.8.2 in /Users/soma/Library/Jupyter/kernels/python3.8.2
```
Now when we start up a new notebook, we can now pick whether we want the default Python 3 kernel or this special Python 3.8.2 kernel! Be sure to use all of the options:

If you don’t use --name, it will overwrite your default python3 kernelspec
If you don’t use --display-name it will be called Python 3 and you’ll get it confused with the default
