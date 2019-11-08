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

# Linux

Key concepts to remember in Linux are:
- How the terminal was invoked changes the environment
- Cron jobs are typically ran limited/no environment
- SSH, a real terminal, and emulated terminals all have different environments
- Command line parameter and environment variable values can be seen by other 
users of the same machine.


Due to the last bullet-point, secrets should never be passed as command line 
arguments or environment variables. STDIN is best when they must be passed.

List all environment variables for current environment `env` or `printenv`
List all running programs with all command line parameters: `ps -auxww`  
List all environment variables for a running process: 
`cat /proc/<process_id>/environ | tr '\0' '\n'`

Try this yourself, it should demonstrate why you should not use environment 
variables or command line parameters for passing secrets.


# Python Environments

## Why Do Python Environments Exist?

If you haven't already, you're likely to run into virtual environments while 
learning python. The reason is, when you're building your Python program you 
will find you are very likely going to install some external libraries using 
`pip`. VirtualENV, PipENV, and others are tools that allows the user to have 
totally different sets and versions of libraries installed all self-contained 
within the virtual environment. This prevents say two applications needing two 
different versions of a library to function properly.

You may believe that you'll never run into this scenario, or if you do you'll 
just fix it yourself, but consider this. What if your operating system used 
python for a critical component like say the system clock? The system clock 
may not seem that important, but if other software on your computer consults 
the system clock this could result in your whole computer not booting. You 
wouldn't want to have to choose between using the latest version of a shared 
library and having your system be able to boot.

This is obviously a contrived example, but it is to point out that sometimes 
what seems unimportant can all of a sudden become critical.

## Import Order

When the Python interpreter sees the `import` keyword, whatever follows is 
imported into the namespace according to where it is found first. For example, 
given the command `import module`, and the sys.path value of 
```
[
    '',
    '/usr/lib/python2.7',
    '/usr/lib/python2.7/plat-x86_64-linux-gnu',
    '/usr/lib/python2.7/lib-tk',
    '/usr/lib/python2.7/lib-old',
    '/usr/lib/python2.7/lib-dynload',
    '/home/chad/.local/lib/python2.7/site-packages',
    '/usr/local/lib/python2.7/dist-packages',
    '/usr/lib/python2.7/dist-packages', 
    '/usr/lib/python2.7/dist-packages/gtk-2.0', 
    '/usr/lib/python2.7/dist-packages/wx-3.0-gtk3'
]
```

Python will iterate over each of these folders looking for `module` until it is 
found. `module` is either going to be in one of these folders as `module.py`, 
or a folder containing `__init__.py`. For example, if my current directory had 
a file of `module/__init__.py`, it would import this file. If not, it would 
continue searching the other folders for the same two files.

When Python is invoked, it automatically prepends PYTHONPATH to the system 
path. Read `python --help` for more details.

```
$ python --help
usage: python [option] ... [-c cmd | -m mod | file | -] [arg] ...
Options and arguments (and corresponding environment variables):
-b     : issue warnings about str(bytes_instance), str(bytearray_instance)
         and comparing bytes/bytearray with str. (-bb: issue errors)
-B     : don't write .pyc files on import; also PYTHONDONTWRITEBYTECODE=x
-c cmd : program passed in as string (terminates option list)
-d     : debug output from parser; also PYTHONDEBUG=x
-E     : ignore PYTHON* environment variables (such as PYTHONPATH)
-h     : print this help message and exit (also --help)
-i     : inspect interactively after running script; forces a prompt even
         if stdin does not appear to be a terminal; also PYTHONINSPECT=x
-I     : isolate Python from the user's environment (implies -E and -s)
-m mod : run library module as a script (terminates option list)
-O     : remove assert and __debug__-dependent statements; add .opt-1 before
         .pyc extension; also PYTHONOPTIMIZE=x
-OO    : do -O changes and also discard docstrings; add .opt-2 before
         .pyc extension
-q     : don't print version and copyright messages on interactive startup
-s     : don't add user site directory to sys.path; also PYTHONNOUSERSITE
-S     : don't imply 'import site' on initialization
-u     : force the binary I/O layers of stdout and stderr to be unbuffered;
         stdin is always buffered; text I/O layer will be line-buffered;
         also PYTHONUNBUFFERED=x
-v     : verbose (trace import statements); also PYTHONVERBOSE=x
         can be supplied multiple times to increase verbosity
-V     : print the Python version number and exit (also --version)
         when given twice, print more information about the build
-W arg : warning control; arg is action:message:category:module:lineno
         also PYTHONWARNINGS=arg
-x     : skip first line of source, allowing use of non-Unix forms of #!cmd
-X opt : set implementation-specific option
file   : program read from script file
-      : program read from stdin (default; interactive mode if a tty)
arg ...: arguments passed to program in sys.argv[1:]

Other environment variables:
PYTHONSTARTUP: file executed on interactive startup (no default)
PYTHONPATH   : ':'-separated list of directories prefixed to the
               default module search path.  The result is sys.path.
PYTHONHOME   : alternate <prefix> directory (or <prefix>:<exec_prefix>).
               The default module search path uses <prefix>/lib/pythonX.X.
PYTHONCASEOK : ignore case in 'import' statements (Windows).
PYTHONIOENCODING: Encoding[:errors] used for stdin/stdout/stderr.
PYTHONFAULTHANDLER: dump the Python traceback on fatal errors.
PYTHONHASHSEED: if this variable is set to 'random', a random value is used
   to seed the hashes of str, bytes and datetime objects.  It can also be
   set to an integer in the range [0,4294967295] to get hash values with a
   predictable seed.
PYTHONMALLOC: set the Python memory allocators and/or install debug hooks
   on Python memory allocators. Use PYTHONMALLOC=debug to install debug
   hooks.
```


## Pip's --user Switch

When installing a package using `pip`, the `--user` parameter can be supplied 
which will indicate to pip to install this package in your home directory. This 
works well for avoiding system-wide issues, but shouldn't be depended on as an 
alternative to a virtual environment.

## Docker

I am currently of the belief that the added complexity of managing virtual 
environments within a docker container is not worth any benefits you may 
receive. If you find this to not be true, please do let me know!

## Anaconda

Anaconda is a collection of data science tools in Python.

When you first install Anaconda, by default, it will modify your terminal to 
start with the default environment activated. Your terminal will be prefixed 
with `(base) `. In Linux this might look like `(base) chad@hostname:~$ `.

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

## PipEnv

PipEnv is an alternative to `virtualenv` that promises to marry `pip` with 
`virtualenv`. It is easier to use and set up than virtualenv as it is a little 
higher level than vitualenv.

Getting going with PipEnv is simple, first install it. You can install pip. 
Note that I recommend installing `pipenv` itself outside of any virtual 
environments for what I hope are obvious reasons. Best practice is probably to 
install this at the user level. `pip install --user pipenv`

To demonstrate, let's give a simple example:

demo.py
```python
from pprint import pprint
pprint('Hello World')
```
Run the following in project directory:
```
pip install --user pipenv
pipenv install pprint
pipenv run python demo.py
```

If done correctly, you should receive the output `Hello World`.

If you want to activate and enter into the virtual environment created, issue 
the command `pipenv shell`. To exit, type `exit` or hit `Ctrl+D`.


Finally, if you want to uninstall packages or remove the environment pipenv 
generated entirely, you do that like this (after exiting the shell of course):

```
pipenv uninstall pprint
pipenv --rm
rm -rf Pipfile*
```


