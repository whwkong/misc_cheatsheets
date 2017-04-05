# setup.py cheatsheet

## Main References 
https://docs.python.org/2/distutils/setupscript.html


## entry points and scripts

<https://chriswarrick.com/blog/2014/09/15/python-apps-the-right-way-entry_points-and-scripts/>

## references for simple cases

<https://learnpythonthehardway.org/book/ex46.html>

    try:
        from setuptools import setup
    except ImportError:
        from distutils.core import setup
        
    config = {
        'description': 'My Project',
        'author': 'My Name',
        'url': 'URL to get it at.',
        'download_url': 'Where to download it.',
        'author_email': 'My email.',
        'version': '0.1',
        'install_requires': ['nose'],
        'packages': ['NAME'],
        'scripts': [],
        'name': 'projectname'
    }
    
    setup(**config)


Click tutorial 
see : <http://click.pocoo.org/5/quickstart/>

Installation

    pip install --editable .

setup.py 

    from setuptools import setup
    
    setup(
        name='HelloWorld',
        version='1.0',
        py_modules=['hello'],
        install_requires=[
            'Click',
        ],
        entry_points='''
            [console_scripts]
            hello=hello:cli
        '''
    )


from ~/dev/test/test\_multifile\_package/: 

    import setuptools
    
    setuptools.setup(
        name='myTestPackage',
        version='0.1.0',
            
        packages=setuptools.find_packages(),
        
        py_modules=['check_mydisk', 'check_system',
                    'check_mysql', 'check_psql',
                    ],
        scripts=[],
        
        install_requires=[
            'Click',
        ],
        entry_points={
            'console_scripts': [
                'check-mydisk = check_mydisk:cli',
            ],
        },
    )


Ben: 
Single file example
<https://github.com/benwebber/curlrc>

    setuptools.setup(
        name='curlrc',
        version='0.2.1',
        url='https://github.com/benwebber/curlrc/',
        
        description="Treat curl configuration files as curlrc subcommands.",
        long_description=open('README.rst').read(),
        
        author='Ben Webber',
        author_email='benjamin.webber@gmail.com',
        
        py_modules=['curlrc'],
        
        zip_safe=False,
        
        entry_points={
            'console_scripts': [
                'curlrc = curlrc:main',
            ],
        },
        
        classifiers=[
            'Development Status :: 4 - Beta',
            "Programming Language :: Python :: 2",
            'Programming Language :: Python :: 2.7',
            'Programming Language :: Python :: 3',
            'Programming Language :: Python :: 3.4',
            'Programming Language :: Python :: 3.5',
        ],
    )


Multiple file example
<https://github.com/vmfarms/pmt/blob/master/setup.py>

    import setuptools
    
    setuptools.setup(
        name='pmt',
        version='0.3.0',
        
        packages=setuptools.find_packages(),
        
        zip_safe=False,
        
        install_requires=[
            'click==6.6',
            'requests==2.11.1',
            'sh==1.11',
        ],
        
        scripts=[
            'bin/pmt',
        ],
        
        classifiers=[
            'Development Status :: 4 - Beta',
            "Programming Language :: Python :: 2",
            'Programming Language :: Python :: 2.7',
            'Programming Language :: Python :: 3',
            'Programming Language :: Python :: 3.4',
            'Programming Language :: Python :: 3.5',
        ],
    )

