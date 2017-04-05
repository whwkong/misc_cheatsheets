# virtualenv cheatsheet 

<https://virtualenv.pypa.io/en/stable/userguide/>
<http://docs.python-guide.org/en/latest/dev/virtualenvs/>

see [virtualfish cheatsheet.md for fish version of virtualenv](./virtualfish\ cheatsheet.md)

## Usage 

Virtualenv has one basic command:

    $ virtualenv ENV

Where `ENV` is a directory to place a new virtual environment. 

The python in your new virtualenv is effectively isolated from the python  
that was used to create it.  

 *** 


### Using virtualenv with different Python versions 
You can also use the Python interpreter of your choice (like python2.7).

    $ virtualenv -p /usr/bin/python2.7 venv

or change the interpreter globally with an env variable in `~/.bashrc`:

    # to use a particular version of Python globally for virtualenv
    $ export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python2.7    

### Other notes

<http://docs.python-guide.org/en/latest/dev/virtualenvs/>

In order to keep your environment consistent, it’s a good idea to   
“freeze” the current state of the environment packages. To do this, run  

    $ pip freeze > requirements.txt   

This will create a requirements.txt file, which contains a simple list of  
all the packages in the current environment, and their respective versions.
You can see the list of installed packages without the requirements format  
using “pip list”. Later it will be easier for a different developer (or  
you, if you need to re-create the environment) to install the same packages  
using the same versions:

    $ pip install -r requirements.txt



### activate script

Activate the shell (separate activate files are available for csh/fish)

	$ source bin/activate			# for bash
    $ . bin/activate                # . = source
    $ source bin/activate.fish		# for fish

Deactivate the shell.

    $ deactivate


Activate changes the $PATH variable so that the first entry is virtuaenv's  
bin/ directory.  It's purely a convenience!  (And also necessary - in
that `path/to/ENV/bin/` takes precedence). 

    $ echo $PATH 
    /Users/thepathunfolds/Temp/HelloWorld/bin etc

The prompt is also changed - this is useful to remind the user which  
virtualenv is being used.  


## Making Environments Relocatable

This is an experimental feature!
 
  *** 

Normally environments are tied to a specific path. That means that you cannot move an environment around or copy it to another computer. You can fix up an environment to make it relocatable with the command:

    $ virtualenv --relocatable ENV


# virtualenvwrapper

<https://virtualenvwrapper.readthedocs.io/en/latest/>
<http://docs.python-guide.org/en/latest/dev/virtualenvs/#virtualenvwrapper>

Note: virtualenvwrapper ONLY runs on bash, ksh, zsh

## installing

<https://virtualenvwrapper.readthedocs.io/en/latest/>
<https://virtualenvwrapper.readthedocs.io/en/latest/install.html>

     $ pip install virtualenvwrapper 
     $ export WORKON_HOME=~/Envs    # see .profile
     


### WORKON\_HOME vs PROJECT\_HOME

What is the relationship between  WORKON\_HOME vs PROJECT\_HOME?
<http://stackoverflow.com/questions/8288297/whats-the-relationship-between-environments-and-projects-in-virtualenvwrapper>
<http://virtualenvwrapper.readthedocs.io/en/latest/command_ref.html#project-directory-management>

    $ mkvirtualenv proj     # 1. creates `proj` virtualenv in $WORKON_HOME

    $ mkproject proj        # 1. creates `proj` virtualenv in $WORKON_HOME
                            # 2. creates `proj` directory in $PROJECT_HOME

Basically, the way virtualenvwrapper works, is that 

1. all virtual environments are placed in $WORKON_HOME 
2. the development directions are placed in $PROJECT_HOME


## Quick-Start/Quick Reference
<http://docs.python-guide.org/en/latest/dev/virtualenvs/>
<http://virtualenvwrapper.readthedocs.io/en/latest/command_ref.html>

    $ workon                # lists or switches environments; equivalent to chdir
    $ mkvirtualenv proj     # creates new virtual env `proj`
    $ lssitepackages        # list site packages for `proj`
    
    $ mkproject proj        # creates virtual env, and a new `proj` directory in 
                            # $PROJECT_HOME
                            
    $ deactivate            # still the same!
    
    $ rmvirtualenv proj     # removes a virtual env
    
    $ lsvirtualenv          # lists all environments
    $ cdvirtualenv          # navigate to directory of currently activated virtual 
                            # environment, to browse the `site-packages`, for example
    $ cdsitepackages        # as above, but directly int `site-packages`


### virtualenvwrapper command reference

<https://virtualenvwrapper.readthedocs.io/en/latest/command_ref.html>





