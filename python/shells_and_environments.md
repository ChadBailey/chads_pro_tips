[comment]: # (Markdown Metadata)
[comment]: # (Intended to use Github markdown processing rules)
[comment]: # (Line width should not exceed 80 for pleasant terminal reading)
[comment]: # (Except when the content is a URL or other continuous data stream)
[comment]: # (-----------------This line is max-width--------------------------)

# Environments

The term `environment` is used in the computer world to collectively describe 
the terminal's environment variables. This design architecture is a rare common 
thread that's shared between all modern operating systems (Windows, MacOS, 
Linux, FreeBSD, Unix, etc.). Environment variables are used to determine many 
arbitrary things typically configuration related. Importantly, this is what 
is typically used for finding other executable files.

Symptoms of an environment related problem are: failure to build, failure to 
import, runs correctly on one computer and not another, runs correctly from 
the command line but not from a scheduled task/cron job.

# Anaconda

Anaconda is a collection of data science tools in Python.

When you first install Anaconda, by default, it will modify your terminal to 
start with the default environment activated. Your terminal will be prefixed 
with `(base) `.

Activate environment using `conda activate`
Deactivate environment using `conda deactivate`


(Recommended) Disable this behavior by issuing the command 
`conda config --set auto_activate_base false`

Install packages into the conda environment by first activating the env 
using `conda activate`, then issuing the `pip install` command replacing `pip` 
with `conda`. For example, `pip install requests` becomes 
`conda install requests`.

> Note that for conda work which uses conda tools such as Jupyter 
> Notebook/IPython you should avoid using the other environment tools for 
> Python such as `virtualenv` or `pipenv`. If instead you are writing Python 
> software which happens to integrate data tools (such as pandas, or numpy),
> then you should not use conda's environment but instead use `virtualenv` or 
> `pipenv` to make distribution easier and dependencies lighter.


