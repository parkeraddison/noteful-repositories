# noteful-repositories
It's time we start storing development notes within our repositories!

**Table of contents**
- [What does it do](#what-does-it-do)
- [How to use](#how-to-use)
- [How it works](#how-it-works)
- [Planned features](#planned-features)

## What does it do

Automatically commits a redacted version of your personal development notes / devlog to the Wiki.

**Motivation**: Personal development notes are crucial for truly understanding how a code repository ended up where it is now. The key directions that the developer had in mind, the approaches they took, and the problems they ran into and tackled or worked around are all things that show up in personal notes, but often don't work their way into a distilled README or technical comments.

It's time we change that, and start shedding more light into the thoughts that contribute to developing a repository. Repositories should be noteful!

## How to use

1. Make sure your repository has a Wiki.
   - You will need to create the first page by using the GitHub website.
2. You should work with personal notes in a markdown file named `Notes.md`.
   - This file should be present in the root directory of your local repository. For file safety, you should probably store the file in a safter directory, and just softlink it to this location.
   - Any information you want redacted from the public version of your notes should be surr
3. Copy the contents of `hooks/` into your `.git/hooks/` directory.

You're done! Now every time you make a commit, a redacted version of your notes will be committed to the repository wiki. Each time you push your repository, the wiki will also be pushed to.

## How it works

Git hooks are scripts that execute at certain stages along the add-commit-push process.

A pre-commit hook is used to verify the structural setup of the notes and wiki.

A post-commit hook is used to add a reference to the commit in your notes for easier searching, and to commit a redacted copy of your notes to the wiki.

A pre-push hook is used to push to the wiki each time you push your repository.

## Planned features

- [ ] Make sure the githooks can play nicely with additional pre-existing (or future) hooks
- [ ] Ensure user doesn't commit their private notes
- [ ] Prompt user for name of notes file; Maybe even create a symlinked file for them
