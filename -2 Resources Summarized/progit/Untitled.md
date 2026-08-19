Think about what a merge actually needs to do.

Suppose your history looks like this:

```text
A---B---C
         \
          D---E   feature
```

and you're currently on `main` at `C`:

```text
A---B---C   main
         \
          D---E   feature
```

Now you run:

```bash
git switch main
git merge feature
```

## The Key Question

Ask yourself:

Does `main` have any commits that `feature` doesn't already contain?

Here, `main` points to `C`, and `feature` is simply a continuation of `C`:

```text
A---B---C---D---E
         ^       ^
        main   feature
```

There is nothing to reconcile.

So Git doesn't need to create a new merge commit.

It can simply move the `main` branch reference forward:

```text
A---B---C---D---E
                 ^
             main, feature
```

That's a fast-forward merge.

## The Perils of Rebasing

Ahh, but the bliss of rebasing isn’t without its drawbacks, which can be summed up in a single line: **Do not rebase commits that exist outside your repository and that people may have based work on.**

Sure — one example:

```text
A---B---C---D---E
             ↑
          shared
```

Alice builds on `E`:

```text
A---B---C---D---E---F
```

Bob then **rebases E**, creating a new `E'`:

```text
A---B---C---D---E'
```

Now Alice has:

```text
A---B---C---D---E---F
```

while the server has:

```text
A---B---C---D---E'
```

`E` and `E'` contain similar work, but they are **different commits**.

So Alice's work is now based on a commit that Bob **rewrote and replaced**. If Alice pulls normally, Git may merge both histories and create a messy history with both `E` and `E'`.

### The rule

**Don't rebase commits that other people have already built their work on.**

- Private commits → rebase freely.
- Shared commits → don't rewrite them.