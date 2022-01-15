# Commit messages

When working on your own smaller projects, less detailed commit messages are okay. But, if you were to ever work for a larger company, such as FAANG, you will be required to write better commit messages.

## Writing good commit messages

A good commit message will consist of a `subject line`, a `body text` and a `footer`. This will result in a commit that clearly describes what was done and why, and is not limited to a certain length.

## Subject line

The subject line should be limited to 50 characters. Keep it short and to the point.  
Don't include capitalization, punctuation, and keep it once sentence.  
It should be written in the imperative, not in past/future tense.
  - Example:
    - "Paint the fence" - good; "Painting the fence" - bad; "Painted the fence" - bad
    - "Make xyz do abc" - good; "This makes xyz do abc" - bad; "Changed xyz to do abc" - bad
    - "Fix bug" - good; "Fixes bug" - bad; "Fixed bug" - bad  

A good subject line will complete the sentence `This commit will ...`  
Optional * - Applies the Angular type  
  - build - changes that affect the build system or external dependencies
  - ci - changes to CI configuration files or scripts
  - docs - documentation only changes
  - feat - a new feature
  - fix - a bug fix
  - perf - improves performance
  - refactor - a code change that neither fixes a bug or introduces a new feature
  - style - changes that do no affect the meaning of the code (eg. white space)
  - test - adding tests or fixing tests
  - debug - for debugging a new idea (console.log, blocking out code, etc.)

## The Body

To add a body to your commit message, instead of typing `git commit -m "message"`, simply type `git commit` to enter into the commit file.

A good body for a commit message:
- No limit in length
- You can go into serious detail about the changes made
- Explain what change you are making
- Explain why you are doing it and in the way you are doing it
- Don't repeat what is obvious from the code diff (the how)
- No need to provide a line by line explanation
- Not always necessary. If it's a small commit, it can likely be explained with just the subject line
- Optional: Limit the line length to 72 characters

