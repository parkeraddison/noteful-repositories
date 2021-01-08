# 'Noteful' repositories: Automatically commit your development notes to a wiki

[![Development notes are in the wiki](https://img.shields.io/badge/notes-in%20wiki-success)](https://github.com/parkeraddison/noteful-repositories/wiki/NOTES)

An open standard for storing development notes along side our repositories. It's time we share our development thought process with future developers!

**Table of contents**
- [What it does](#what-it-does)
- [Why it does](#why-it-does)
- [How to use](#how-to-use)
- [How it works](#how-it-works)
- [Planned features](#planned-features)
- [Contributing](#contributing)
- [Notes](#notes)

## What it does

Automatically commits a redacted version of your personal development notes / devlog to the Wiki.

## Why it does

Personal development notes are crucial for truly understanding how a code repository ended up where it is now: The *key directions* that the developer had in mind, the *approaches* they took, and the *problems* and *workarounds* they ran into.

These show up in personal notes and -- within the indie game communities -- within public dev logs. But the vast majority of code repositories do not express such information. It's time we change that.

By incorporating deverlopment notes along side our repositories, we build a community knowledge of hardships during the development process and shed more light into the thoughts that contribute to developing a repository. Repositories should be noteful!

## How to use

1. Make sure your repository has a Wiki.
   - You will need to create the first page by using the GitHub website.
2. Keep your development notes in a markdown file named `Notes.md`.
   - This file should be present in the root directory of your local repository. For file safety, you should probably store the file in a safter directory, and just softlink it to this location.
   - Any information you want redacted from the public version of your notes should be surrounded by curlybrackets and tildes: `{~this would be redacted~}`
3. Copy the contents of `hooks/` into your `.git/hooks/` directory.
4. Paste the following badge into your main README file to let others know where your notes are (substitute your user and repository names)
   - ```md
     [![Development notes are in the wiki](https://img.shields.io/badge/notes-in%20wiki-success)](https://github.com/<your_user>/<your_repo>/wiki/NOTES)
     ```

You're done! Now every time you make a commit, a redacted version of your notes will be committed to the repository wiki. Each time you push your repository, your notes will also be pushed to the the wiki.

## How it works

Git hooks are scripts that execute at certain stages along the add-commit-push process, and GitHub Wikis (and GitLab Wikis) are actually just separate repositories with the remote url `<main_project_url>.wiki.git`! Therefore we can just commit our notes to the wiki every time we make a commit in our main repository.

That's exactly how it's done:

1. A pre-commit hook is used to verify the structural setup of the notes and wiki.

2. A post-commit hook is used to add a reference to the commit in your notes for easier searching, and to commit a redacted copy of your notes to the wiki.

3. A pre-push hook is used to push to the wiki each time you push your repository.

Components (1) and (2) happen each time you make a commit in any branch of your local repository, and (3) happens whenever you push to your remote repository.

## Planned features

- [ ] Make sure the githooks can play nicely with additional pre-existing (or future) hooks
- [x] ~~Ensure user doesn't commit their private notes~~ -- should already be acomplished by .gitignore configuration
- [ ] Automatically detect potentially sensitive info (e.g. email addresses) and prompt for redaction
- [ ] Prompt user for name of notes file; Maybe even create a symlinked file for them
- [ ] Add more prompts throughout -- e.g. prompt if Wiki needs to be created on site
- [ ] Prompt user to add notes badge into README

## Contributing

Yes, please!

## Notes

This repository itself is a noteful repository. [Development notes can be found in the wiki](https://github.com/parkeraddison/noteful-repositories/wiki/NOTES).
