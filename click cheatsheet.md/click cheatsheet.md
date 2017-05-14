# Click Notes

see : https://click.pocoo.org



## Overview of Groups and Commands


You can think of groups and commands as folders and files respectively. 

A group is actually an [MultiCommand](http://click.pocoo.org/6/api/#click.MultiCommand) 

Commands are always endpoints; groups can contain commands and other 
sub-groups.  Options are always passed via -o, --option syntax.  Note that Groups can have options passed to it. 

    @click.group()
    @click.option('--debug/--no-debug', default=False)
    def cli(debug):
        click.echo('Debug mode is %s' % ('on' if debug else 'off'))
    
    @cli.command()
    def sync():
        click.echo('Synching')


## Customizing Command Names

    cli.add_command(schedule)
    cli.add_command(sim)
    schedule.add_command(create, name='custom_name')

## Customizing Parameter Names

http://click.pocoo.org/5/parameters/#parameter-names
For an option with ('-f', '--filename', 'dest'), the parameter is called dest.

    @click.command()
    @click.option('-d', '--day', 'weekday', # weekday becomes default param name
                  default=datetime.datetime.today().isocalendar()[2],
                  help='isoday.  Defaults to current isoday')
    def day(weekday):
        pass


## Nested Handling and Contexts

If a parameter is passed to a group, that parameter is not normally passed to a subcommand, unless a `Context` is used.
see : http://click.pocoo.org/6/commands/#nested-handling-and-contexts

    @click.group()
    @click.option('--debug/--no-debug', default=False)
    @click.pass_context
    def cli(ctx, debug):
        ctx.obj['DEBUG'] = debug
    
    @cli.command()
    @click.pass_context
    def sync(ctx):
        click.echo('Debug is %s' % (ctx.obj['DEBUG'] and 'on' or 'off'))
    
    if __name__ == '__main__':
        cli(obj={})


## Groups can be invoked without a Command

Back to the Group/Command and folder/file metaphor, normally a Group cannot be invoked like a sub-command, unless the `invoke_without_command=True` is passed to a group.  

see : http://click.pocoo.org/6/commands/#group-invocation-without-command

    @click.group(invoke_without_command=True)
    @click.pass_context
    def cli(ctx):
        if ctx.invoked_subcommand is None:
            click.echo('I was invoked without subcommand')
        else:
            click.echo('I am about to invoke %s' % ctx.invoked_subcommand)
    
    @cli.command()
    def sync():
        click.echo('The subcommand')

## Merging Multi Commands (Groups) dynamically 

see :http://click.pocoo.org/6/commands/#merging-multi-commands
Groups of commands can be merged (collapsed) into the same hierarchy level.  

    import click
    
    @click.group()
    def cli1():
        pass
    
    @cli1.command()
    def cmd1():
        """Command on cli1"""
    
    @click.group()
    def cli2():
        pass
    
    @cli2.command()
    def cmd2():
        """Command on cli2"""
    
    cli = click.CommandCollection(sources=[cli1, cli2])
    
    if __name__ == '__main__':
        cli()

And what it looks like:

    $ cli --help
    Usage: cli [OPTIONS] COMMAND [ARGS]...
    
    Options:
      --help  Show this message and exit.
    
    Commands:
      cmd1  Command on cli1
      cmd2  Command on cli2


## Command Chaining
see : http://click.pocoo.org/6/commands/#multi-command-chaining

Command chaining is the act of chaining multiple commands that exist within
the same group hierarchy.  

    @click.group(chain=True)  # chain paramter is set to True
    def cli():
        pass
    
    @cli.command('sdist')
    def sdist():
        click.echo('sdist called')
    
    @cli.command('bdist_wheel')
    def bdist_wheel():
        click.echo('bdist_wheel called')


## Multi-Command Pipeline

Simply the ability of one command to process the result of the previous command.  (This is at the same level of group hierarchy), and probably unnecessary for most applications.)








