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

### `Part N` rewriting

If your commit message contains the string `"Part N"`, it will be rewritten to
contain the correct part number. For example if you write the commit messages:

```
Bug 100 - Part N: Cheese
Bug 100 - Part N: Pear
Bug 100 - Part N: Apple
Bug 100 - Part N: Coconut
```

The messages will be rewritten to:

```
Bug 100 - Part 4: Cheese
Bug 100 - Part 3: Pear
Bug 100 - Part 2: Apple
Bug 100 - Part 1: Coconut
```

## How it Works

The script generates a small python script which will look up, based on the
commit message passed over stdin, the commit message you wrote. It will then
pass this script as an `msg-filter` to `git filter-branch`.
