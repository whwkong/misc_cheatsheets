# python debugger

Install pdb++ 
https://pypi.python.org/pypi/pdbpp/


## Tutorials 

pdb tutorial 
http://stackoverflow.com/questions/4228637/getting-started-with-the-python-debugger-pdb

I like this one a lot : 
https://pythonconquerstheuniverse.wordpress.com/2009/09/10/debugging-in-python/


## Instructions

see <http://stackoverflow.com/questions/4929251/can-you-step-through-python-code-to-help-debug-issues>

https://docs.python.org/3/library/pdb.html

The typical usage to break into the debugger from a running program is to insert

	import pdb; pdb.set_trace()


## Common pdb commands

	b  		- set a breakpoint
	c		- continue debugging until you hit a breakpoint
    
	s		- step through code
    r       - return; continue to the end of the subroutine
    
	n		- next line
	l		- list source code (default : 11 lines)
    ll      - longlist, current line is marked with '->'
	u		- navigate up a stack frame (step up)
	d		- navigate down a stack frame (step down)
	p		- print the value of an expression
    
    w(here) - Print a stack trace, with the most recent frame at the bottom.
    
    tbrea   - Temporary breakpoint, which is removed automatically when it is first hit.




## Methods to enter Python 'pdb'

1. Within your program
 
	import pdb; pdb.set_trace()

2. From Command Line
 
	$ python -m pdb <script-name.py>






