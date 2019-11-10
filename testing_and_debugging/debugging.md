# Python

## Import Python Debugger

If you must debug server-side, insert this snippet anywhere in your code to 
break out into an interactive command line debugging prompt 
`import pdb;pdb.set_trace()`

To take this a step further, you can encapsulate your code like this

```Python
try:
    code_goes_here
except:
    import pdb;pdb.set_trace()
```

This will enter an interactive debugger when an exception is hit. You can go up
in the stack trace, issue commands, etc.

### PDB Command Quick Ref

| Command       | Description                                       |
|---------------|---------------------------------------------------|
| `quit`        | abort program execution                           |
| `return`      | exit after return of current function             |
| `continue`    | exit interactive debugger, continuing execution   |
| `step`        | steps into next function call                     |
| `next`        | steps over next function call                     |
| `up`          | moves up the call stack                           |
| `down`        | moves down the call stack                         |

