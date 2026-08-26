> an ACTOR is an active agent which plays a role on cue according to a script

([A Universal Modular ACTOR Formalism for Artificial Intelligence, 1973](https://www.ijcai.org/Proceedings/73/Papers/027B.pdf))

Nervous Notes is a Python module for managing _actors_ that have an associated plaintext Markdown note for their memory. 
Each Markdown note can have YAML at the start, gated with `---` on the lines before and after the YAML. 

**There is no AI in this project**, the notes are "nervous" because the actor model allows them to _reflexively_ react to 
events, like their note being modified by a human, or a message sent by another note. If someone wants the "reflex" to 
be an AI invocation, they are free to do so.

Useful for
- hot-reloadable daemons with plaintext, human-friendly memory
- [literate programming](https://en.wikipedia.org/wiki/Literate_programming) (Knuth, 1984) and "knowledge based programming" (same 1973 paper)
- personal knowledge management (e.g. automating some of an Obsidian vault)

## Quick Start

```commandline
pip install nervous-notes
```

`python -m` to `example_scripts` FIXME

example note FIXME
```
---
this_is: yaml
---
- (markdown)
```

## Glossary

- FIXME
- companion
- embedded - for literate programming
- actor / agent
- note / nervous note

## Standard event types

- FIXME (placeholder)
  - note updated
  - timer up
  - mqtt message
  - "other" pykka message

## Note API

- FIXME (placeholder)

## Polyglot programming

This module currently includes mqtt support, which allows for sending messages between programs in different languages.

## Knowledge Based Programming

Again, from the actor model paper:

> KNOWLEDGE BASED PROGRAMMING is programming in an environment which has a substantial knowledge base in the application area for which the programs are intended.

## Limitations

- Pykka's thread/GIL limits are inherited
  - multiprocessing support is limited and experimental
- globals are shared between hot-reloaded **embedded** nervous notes
- if someone removes a function from a hot reloading script, they should replace it with `pass` in the body before removing it, or else the prior version will remain active
- there are currently no built-in circuit breakers

### Interfacing with Obsidian

I found that updating a note _immediately_ after a note-modified event can cause Obsidian to ignore the update, so there
are some sleep() calls to accommodate the behavior.

## History

I originally implemented this in Scala, where I called it "[woke notes](https://github.com/micseydel/tinker-casting/tree/main/scripts/woke_notes_package)" before spinning off this fully separate repo.

## Future work

- remove mqtt as a default dependency, and make it, kafka, and rabbitmq [optional dependencies](https://setuptools.pypa.io/en/latest/userguide/dependency_management.html#optional-dependencies)
  - maybe a "whisper" optional dependency for AI transcription (since this was one of my primary use-cases)
- similar modules for other languages/platforms (e.g. JVM, Javascript, Go, etc.) to improve polyglot support
- is Obsidian Canvas rich enough to wire actors together into flows?
- improved isolation between companion notes
- replace blocking I/O with non-blocking
- replace Pykka with something more Akka-like
  - this would likely be an _enormous_ undertaking
