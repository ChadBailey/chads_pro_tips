# File Transfer

## Magic Wormhole

[Magic Wormhole](https://github.com/warner/magic-wormhole) is a utility written 
in python that makes transferring files from computer to computer 
fast/easy/secure/painless.

The docs are a bit unnecessarily verbose, here's what you need to know

### Installation via PyPi (if you have Python installed)

> Requires Python installed and in your path
> Windows requires Python 2.7

`pip install magic-wormhole`

### Installation via OS specific instructions

Alternately, you can install via your OS specific installation instructions 
which are available in the 
[install docs](https://magic-wormhole.readthedocs.io/en/latest/welcome.html#installation).

### Usage

1. Use via `wormhole send file-or-folder`
  > If you specify a folder it automatically zips it for you
2. It will prompt you the receive instructions for the target machine i.e.
```
Sending directory (10.2 MB compressed) named 'example'
Wormhole code is: 9-pandemic-dropper
On the other computer, please run:

wormhole receive 9-pandemic-dropper
```
3. Enter the prescribed code on the target PC to receive the file. i.e. 
`wormhole receive 9-pandemic-dropper`

> Codes can only be used once, so if there are any complications repeat the 
process
