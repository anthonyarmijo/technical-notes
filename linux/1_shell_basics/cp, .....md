[[_The Linux Command Line | Back to Home]]
___
## Copy with cp

```bash
# standard copy syntax
cp /dir/somefile /somedir
```

```bash
# use cp -a to copy all files (including hidden files), but use the .* wildcard to include hidden files as well.
cp -a ~/.* /tmp/
```
* Regarding the above example, note that `tar` is a better solution to archive hidden files

```bash
# 'Recursive' copy to include subdirectories
cp -R
```

___
[[_The Linux Command Line | Back to Home]]