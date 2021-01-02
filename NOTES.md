# Noteful repositories

###### 01/01/2021

The basic idea I have is this:

- Add pre-commit hook so that a Notes.md file in the repository is preprocessed (sensitive information can be redacted) and added to each commit
- Add hook during pulling so that non-redacted changes are preferred... I don't know how this'll be done yet.

These hooks could probably be added to any repository (in the `.git/hooks` directory so they're not version controlled) in order to make it a noteful repository!

What would be even cooler is if upon committing (or pushing to GitHub and use Actions) a search index is generated (or a pre-trained model encodes the text) to make the notes more easily searchable or enable semantic search!

## Redaction

Can probably use a simple sed script. I'm 'introducing' a new markdown syntax of ` [REDACTED] ` -- namely because it's easy to make regex patterns for eager pair matching, and Typora (and other editors) do auto-pairing for curly braces, which makes it quick and easy to type. And -- to my knowledge -- I don't think ` [REDACTED] ` is too common in languages, so it hopefully shouldn't show up in code snippets.

Normally the pattern ` [REDACTED] ` with the `g` and `s` options would be enough -- `s` tells regex to include newlines in dot. But sed doesn't accept the `s` option!

https://stackoverflow.com/questions/8624283/how-to-tell-sed-dot-match-new-line

Aaaaand it also doesn't handle non-greedy (lazy) matches!

https://unix.stackexchange.com/questions/128362/lazy-regex-using-bash

But `perl` does! I just don't know if it's included in GitBash by default (it would be nicest if the only requirement was GitBash itself)

I'm having some issues though with the multi-line stuff still.

https://www.systutorials.com/how-to-match-multiple-lines-using-regex-in-perl-one-liners/

Which I can resolve by adding the `-0` flag (even without any arguments)

The (close to) final result

```bash
perl -0 -pe 's/ [REDACTED] / [REDACTED] /gs' infile
```

it might be fun to use full blocks █ for redaction. But they might be annoying too!

I'd like to be able to escape the pattern too. New pattern just uses a couple negative lookbehinds for this: `(?<!\\) [REDACTED] `

