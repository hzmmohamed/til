---
date: 15-02-2022
title: Highlights from the IPython docs
tags: ['jupyter', 'python', 'notebook']
---


Somehow, I found it quite easy to digest, for the most part. Maybe that's because I've been exposed to the basics a long time ago. In this entry, I document, for my future self, that I have gone through all the documentation pages. 


## Architecture

[IPython](https://ipython.readthedocs.io/en/stable/) is not just a REPL. It has a different architecture.

>IPython has abstracted and extended the notion of a traditional Read-Evaluate-Print Loop (REPL) environment by decoupling the evaluation into its own process. We call this process a kernel: it receives execution instructions from clients and communicates the results back to them.

Running `ipython` in the terminal spawns a traditional single-process environment. However, when starting a `jupyter notebook` or `jupyter qtconsole`, you are starting two processes, a kernel and a client.

This decoupling of kernel and client allows multiple clients to connect to one kernel, and allows them to be living on different machines. There's a [message spec](https://jupyter-client.readthedocs.io/en/latest/messaging.html#messaging) that defines communication between kernels and clients.


## Highlights
I gather highlights from IPython's for later reference.
### Connection Info
Use `%connect_info` to get a JSON object that describes the kernel connection. It can be passed to a new client to connect to the same kernel.

### Rich Output
Print any object with a rich output using `from IPython.display import display`

### Change matplotlib backend
Using the `%matplotlib <backend>` magic command.

### Information about objects
`?` is used to get information about an object. Such information (docstring, constructor, etc.) changes based on the type of the object. `??` shows more/detailed info.

### Timing Functions
`%timeit` time a single line. `%%timeit` times a whole cell.


### Inspecting the interactive variables
`%who_ls` returns a sorted list of interactive variables. `%whos` prints interactive variables with more information (type and value)

## Other Notes
- I was trying to find a way to cache a cell's output in memory, so that running it again doesn't actually re-run it. This would be useful for reading a large dataset into memory, or for joins that take a long minutes. I couldn't find a magic command that does that. There's a command for saving the output into a file.

