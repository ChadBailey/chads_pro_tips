# Visual Studio Code Overview

Visual Studio Code is a general purpose IDE. It is Free and Open Source, 
distributed by Microsoft. It has an excellent default set of features with 
a large extension library.

I recommend Visual Studio Code for being light weight, FOSS, and supporting 
a wide assortment of languages.

## Workspaces

A workspace is what VSC uses to refer to what you might know as a "session" 
in browser terms. That is to say, the currently open tabs/files/folders.

In VSC, a workspace can be saved and recalled. Every time VSC is opened it 
automatically reopens its previous session, whether the session has been 
saved or not and whether the unsaved files or changes you were making were 
saved or not.

It is worth mentioning that as of the time of writing this will behavior does 
not work properly when VSC quits with multiple sessions open at once. In my 
experience, if you have multiple sessions opened at once it will either not 
open any session or open the one last interacted with.


# Settings

[Official Docs](https://code.visualstudio.com/docs/getstarted/settings)

VS Code has 2 scopes of settings, `User` and `Workspace`. A setting scoped to 
`User` is a global setting. A setting scope to `Workspace` only applies to 
that specific workspace and overrides the global `User` scoped settings.

Most settings changes are performed via `File > Preferences > Settings`.

User scoped settings are stored in a different place depending on your OS. 
Here is a list of where this settings file can be found.

- Windows `%APPDATA%\Code\User\settings.json`
- macOS `$HOME/Library/Application Support/Code/User/settings.json`
- Linux `$HOME/.config/Code/User/settings.json`

Workspace scoped settings are stored in a folder generated at the root-level 
of the project `.vscode/settings.json`.



# Useful hotkeys

| Description               | Hot Key               |
| ------------------------- | --------------------- |
| Zoom out                  | `Ctrl -`              |
| Zoom in                   | `Ctrl +`              |
| Markdown preview          | `Ctrl+Shift+V`        |
| Markdown live preview     | `Ctrl+K V`            |
| Multi-line cursor         | `Ctrl+Shift+Arrow`    |

# Recommended Addons

- GitLens
- Code Spell Checker

# Add Column Ruler

Reference 
[this](https://stackoverflow.com/questions/29968499/vertical-rulers-in-visual-studio-code) 
stack overflow question/answer for more details.

In this example, I will be showing you how to add rulers at column 80 and 120. 
If you want to add more, just adjust `[80,120]` to include your desired rulers 
using a comma-separated list. For example: `[80,120,100]`. If you only want a 
single ruler, just remove the commas all together, like `[80]`.

Visit `File > Preferences > Settings` and search for "rulers". Find the 
following section:

> Editor: Rulers
> 
> Render vertical rulers after a certain number of monospace characters. Use 
> multiple values for multiple rulers. No rulers are drawn if array is empty.
> 
> Edit in settings.json

Click on the `Edit in settings.json` link below it. This should open a JSON 
settings editor. Add the line `"editor.rulers": [80,120]` to the bottom of the 
JSON file, but within the curly-braces. Your file should look something like 
this, depending on what other settings you have adjusted:

```JSON
{
    "git.autofetch": true,
    "editor.rulers": [80,120]
}
```

# Configuration

To begin debugging the current file, hit `F5` or click 
`Debug > Start Debugging`. This will cause a dropdown to appear with known 
options for debugging the file. To choose a default option so that debugging is 
instant, click `Debug > Add Configuration`. This will save a file in 
`.vscode/launch.json`.

> IMPORTANT: I have personally seen exploits in the wild searching for .vscode 
and related files, so please add this to your gitignore and do not expose to 
any web servers. Apparently, some configurations will store passwords here.

## Behave Cucumber Testing (Python)

In order to debug .feature files using behave, you must add your own custom 
debugger. Do this by going to `Debug > Add Configuration` Next, click `Python` 
then `Module`. Enter `behave` into the prompt then hit enter. `launch.json` 
should now be shown with an entry for behave. Here is an example:

```JSON
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Module",
            "type": "python",
            "request": "launch",
            "module": "behave"
        }
    ]
}
```