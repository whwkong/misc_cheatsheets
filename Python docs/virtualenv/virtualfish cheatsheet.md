# virtualfish cheatsheet

see <https://hackercodex.com/guide/tacklebox-fish-shell/#python-virtual-environments>
see <http://virtualfish.readthedocs.io/en/latest/>

## Customizing Your fish_prompt

see <http://virtualfish.readthedocs.io/en/latest/install.html#customizing-your-fish-prompt>


## virtualfish Usage
http://virtualfish.readthedocs.io/en/latest/usage.html

    vf new your-virtual-env-name        # create virtual environment in ~/Virtualenvs/
    
    vf project your-project-name        # creates new project in ~/Projects 
                                        # and a new virtual environment in ~/Virtualenvs/
                                        
    vf ls                               # list all virtualenvs
    vf activate <envname>               # activate a virtualenv.                                
    vf deactivate                       # deactivate the current virtualenv
    vf rm <envname>                     # delete virtualenv
    
    vf cd                               # chdir to currently-activated virtualenv
    vf cdpackages                       # chdir to the currently-activated virtualenv’s site-packages.
    
    vf addpath                          # Add a directory to this virtualenv’s sys.path
    vf all <command>                    # Run a command in all virtualenvs sequentially. 
    
    vf connect                          # Connect the current working directory with the 
                                        currently active virtualenv. This requires the 
                                        auto-activation plugin to be enabled in order to 
                                        have any effect besides creating a .venv file in 
                                        the current directory.



                                        
    workon your-project-name            # workon project and activate its virtual environment


### Using Different Pythons

see <http://virtualfish.readthedocs.io/en/latest/usage.html#using-different-pythons>




