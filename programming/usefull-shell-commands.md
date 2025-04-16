# Useful shell commands

Also the obvious ones, I guess.

## Command combinations

### Don't remember command used before?

Search through your `bash_history` and get the lines that contain the text you're looking for with

```sh
cat ~/.bash_history | grep python
```

or search you python repl for when you used a file.

```sh
cat ~/.python_history | grep -C 5 'filename'
```

### Count number of matches

```sh
cat file | grep match | wc -l
```

## Single commands

### cat

Print the contents of the file

### ls - list

```sh
ls -l  # also shows symlinks nicely!
```

### mkdir - make directory

Automatically create parent directories if needed, without error if they already exist

```sh
mkdir -p directory
```

### mv - move

`to` can be either a new filename or a directory

```sh
mv from to
```

### cp - copy

You can copy symbolic links as they are by using arguments, `-pPR`, or

```sh
cp -a
```

### grep

```sh
echo 'whatever' | grep 'glob'
```

If you want the surrounding lines, known as context, there are the options `-A num`, `-B num` and `-C num` for also showing `num` lines after the match, before the match, or both respectively.

```sh
cat ~/.python_history | grep -C 5 'filename'
```

### sed

Find and replace.

### ln - link

```sh
ln -s  # For symbolic (soft) links, hard links without -s
```

### realpath

For turning a relative path into a full path, useful for [`ln`](#ln---link)

> very nice program. But note that it is an external command (not a shell built-in) and may not be present in every system by default, i.e. you may need to install it. In Debian it resides in a separate package with the same name. [(source)](https://stackoverflow.com/questions/3915040/how-to-obtain-the-absolute-path-of-a-file-via-shell-bash-zsh-sh#comment4176981_3915075)

### wc - word count

Also for line count

```sh
cat file | wc -l
```

### du - disk utility

Create a sorted list of how much space is used by each file/directory

```sh
du -sh directory
```

### tar - tarball

Create an archive from files, possibly excluding files and directories matching any of the `--exclude` args.

This is an example I used for zipping a Minecraft data/resource pack, before learing this wouldn't work in game.

```sh
tar --exclude '*entity*' --exclude '.DS_Store' -czvf "UNZIP_ME___Spawn_Egg_Masks_resourcepack.tar.gz" 'Spawn Egg Masks/'
```

### zip

Because Minecraft resource packs can be zip files only. You should prefer `tar` usually since that's better compression
by default, due to combining all the data before compressing instead of deflating each file individually with zip.

```sh
zip 'VSGFL.zip' -r 'assets' pack.png pack.mcmeta -x '*/.DS_Store'
zip 'Spawn Egg Masks [datapack].zip' -r 'data' pack.png pack.mcmeta -x '*/.DS_Store' '*entity*'
```
