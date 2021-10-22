pre-commit-hooks
================

Some hooks for pre-commit.

See also: https://github.com/pre-commit/pre-commit


### Using pre-commit-hooks with pre-commit

Add this to your `.pre-commit-config.yaml`

```yaml
-   repo: https://github.com/pawsen/pre-commit-hooks
    rev: v1.0
    hooks:
    -   id: prepare-commit-msg
    # -   id: commit-msg, ... etc
```

The hooks are stored in `~/.cache/pre-commit/` after running `pre-commit`.


See also
```
pre-commit clean
pre-commit uninstall
pre-commit autoupdate
```

### Hooks available
#### `prepare-commit-msg`
Use this

#### `commit-msg`
And probably not this

### Adding new hooks

Add new hooks to `.pre-commit-hooks.yaml` and test them by running `pre-commit
try-repo ~/path/to/pre-commit-hooks` from a folder with files you want to test
the hook on.

As an example, let's test the `prepare-commit-msg` hook 

(NOTE: `prepare-commit-msg` is both a `hook-stage` and the id of this particular
hook.)

```
mkdir -p ~/tmp/hook-test && cd ~/tmp/hook-test
git init
git checkout -b feature/00001_the_very_first_branch
# ensure ref HEAD is defined
git commit --allow-empty -n -m "Initial commit."

pip install --user pre-commit

# hook-stage commit-msg & prepare-commit-msg needs the the path to a file with
# a commit-msg
echo "This is my commit msg" > commit.msg
pre-commit try-repo --hook-stage prepare-commit-msg --verbose --commit-msg-filename ./commit.msg ~/git/pre-commit-hooks prepare-commit-msg

cat commit.msg
```

with `try-repo` you don't need to point to a specific revision.


When satisfied, push the changes and update the tag
```
git tag -f v1.0 && git push --tags -f
```
