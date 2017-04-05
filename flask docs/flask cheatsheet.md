# flask notes 

http://flask.pocoo.org/docs/0.12/

## flask tutorials

- https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-xv-ajax


## Larger Application Patterns
http://flask.pocoo.org/docs/0.12/patterns/packages/#larger-applications


## vmfarms flask projects

https://github.com/vmfarms/topsoil


## Logging, and Logging configuration


Currently unable to get configuration file working, but I can dynamically add 
a handler to app.logger object. 

    # from https://docs.python.org/3/howto/logging.html#configuring-logging
    logging.config.fileConfig('logging.conf')
    ch = logging.StreamHandler()
    ch.setLevel(logging.DEBUG)
    formatter = logging.Formatter('%(asctime)s : %(name)s : %(levelname)s : %(message)s')
    ch.setFormatter(formatter)
    app.logger.addHandler(ch)

Another option is to use a custom configuration file 

see : http://flask.pocoo.org/snippets/2/
see : http://stackoverflow.com/questions/11816236/how-to-config-flask-app-logger-from-a-configure-file
  - doesn't solve the problem; but adds background info.


## Useful Extensions

### flask-script

If you need to execute some code after your flask application is started but 
strictly before the first request, not even be triggered by the execution of 
the first request as @app.before_first_request can handle, you should use 
Flask Script

https://flask-script.readthedocs.io/en/latest/

- http://stackoverflow.com/questions/27465533/run-code-after-flask-application-has-started
- http://stackoverflow.com/questions/9276078/whats-the-right-approach-for-calling-functions-after-a-flask-app-is-run
  - alternate solution






