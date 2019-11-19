# Fix stuff

Reset entire terminal (fixes most issues): `reset`

Clear console: `clear`

Exit shell (will return to prior environment if you were in a sub-shell): `Ctrl+D`

Clear input: `Ctrl+U`
> Useful when typo'd password and don't know how many times to backspace


# Task management

Send active task to background (execution paused): `Ctrl+z`

```
$ top

[1]+  Stopped                 top
```

See background tasks: `jobs`

```
$ jobs
[1]+  Stopped                 top
```

Allow task to continue running in the background: `bg %1`
> %1 indicates job number 1

```
$ bg %1
[1]+ top &
```

Kill first job: `kill %1`

```
$ kill %1

[1]+  Stopped                 top
```

