# Remotely debugging a JAR

At times, there arises a need to debug code deployed somewhere remotely in the form of a JAR, as some issues
may not be diagnosable locally.

## Command to run JAR with debug mode enabled

```bash
java -Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address=*:5005 -jar <NAME-OF-JAR-FILE>\
Listening for transport dt_socket at address: 5005
```

On `zsh`, the `*` needs escaping (`\*`).

Answers on StackOverflow claim this is the legacy way of running the JVM debugger with worse performance
than modern ways, but the command above should be good enough. (May be worth investigating the morden way
at some point).

## Attaching to remote debugger from IntelliJ

The exact placement and phrasing of buttons may change with future releases of IntelliJ. As of 2022:
Run -> Edit Configurations -> Add new configuration (+ icon) -> Remote JVM Debug -> change name to something
descriptive and click OK.

Now, Run -> Debug 'name-of-configuration'. Make sure to have set a breakpoint somewhere in the code.
As long as a connection can be established, IntelliJ should report:
```
Connected to the target VM, address: 'localhost:5005', transport: 'socket'
```
and the application in the JAR should start up.

Now the remote application's code can be stepped through, just as it can be done locally.
