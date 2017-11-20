# git rmsg

This is a simple script which makes it easier for me to batch-rewrite the first
lines of my commit messags.

## Usage

```bash
$ git rmsg SHA
```

This will pop up your `$EDITOR` with the first lines of commit messages of the
commits between `SHA` and `HEAD`. Edit that file, changing each commit's name to
the desired name, and exit your editor. `git rmsg` will then rewrite history,
changing the name of each of these commits to the name you provided.

Lines following the first line in each commit message will be preserved without
changes.

## How it Works

The script generates a small python script which will look up, based on the
commit message passed over stdin, the commit message you wrote. It will then
pass this script as an `msg-filter` to `git filter-branch`.
