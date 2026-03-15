---
tags:
  - opensource
  - GSOC2026
  - round1
---

Hello everyone! 

[I've been looking into kitty's text-sizing-protocol](https://github.com/kovidgoyal/kitty/blob/master/docs/text-sizing-protocol.rst)

and whether it can be useful in the proposed [presentation mode](https://github.com/neovim/neovim/issues/31825)

has anyone worked/working on this currently? 
also is there is any known limitations or ideas on how we can work this through? 

from really high-level I imagine it as an optional opt-in feature,
that will have a lua API (maybe in vim.api.keyset.highlight) for changing buffer font size if supported in the terminal.

is changing the API in this manner acceptable? assuming its following the standard and terminal agnostic? 

Iam new to neovim contributions so i would appreciate all the feedback!