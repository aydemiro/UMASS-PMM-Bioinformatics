### File system disk usage analysis with df
Please read the manual of du command with ```man df``` for indepth information on this command.  

You can use ```df``` command to see the disk usage at file system level. This is useful to learn how much space is used/available in a given mount point. Example mount points are:  
1) Your groups project space
2) Your home space
3) Your groups nearline space

Use with ```-h``` option for human readable values (GB, MB, etc)

Example:
```bash
df -h /project/umw_john_doe

# Filesystem            Size  Used Avail Use% Mounted on
# umassmghpcc-head.umassrc.org:/ifs/xdata/project/umw_john_doe
#                       2.0T  1.8T  108G  95% /project/umw_john_doe
```

Note that it is not immediately clear what the 2.0T value represent, for example, because that information is not present in the line above the numbers, but 2 lines above (Size). 

### Disk usage analysis with du
Please read the manual of du command with ```man du``` for indepth information on this command.  

You can use ``du`` command to estimate disk usage of a given directory and its subdirectories. This is useful when you want to know how much space a certain directory is taking up.  
Use with ```-h``` option for human readable values (GB, MB, etc).

Example:

Find disk usage in ```/project/umw_john_doe/folder```
```bash
du -h /project/umw_john_doe/folder

# 50K /project/umw_john_doe/folder/subdir1/subsubdir1
# 40M /project/umw_john_doe/folder/subdir1
# 30M /project/umw_john_doe/folder/subdir2/subsubdir2
# 400M /project/umw_john_doe/folder/subdir2
# ...
# 2G  /project/umw_john_doe/folder
```
In many cases the output of this command will be very long and the size of each and every subdirectory (and their subdirectories (and their subdirectories (..))) is not wanted. To find disk usage in ```/project/umw_john_doe/folder``` without listing its subdirectories use ```-s``` option:
```bash
du -h -s /project/umw_john_doe/folder

# 2G  /project/umw_john_doe/folder
```
In yet more cases, you may want to document disk usage at a level between these two extremes. In that case you can use `--max-depth` option followed by the number of levels you want to analyse. For example, to get disk usage of  ```/project/umw_john_doe/folder``` and its first level subdirectories:
```bash
du -h --max-depth 1 /project/umw_john_doe/folder

# 40M   /project/umw_john_doe/folder/subdir1
# 400M  /project/umw_john_doe/folder/subdir2
# 400M  /project/umw_john_doe/folder/subdir3
# ...
# 2G    /project/umw_john_doe/folder
```

Note that the `-s` option is equivalent to `--max-depth 0` option.  

By default the command output is displayed on the screen which is temporary and can be very long -you'll only see the last lines of the output. You can use output redirection to save the command output (and the error) to files. For example, to find disk usage in ```/project/umw_john_doe/folder``` and its first level subdirectories and send output to a file named `du.out` in your home directory and error messages a file named `du.err`:
```bash
du -h --max-depth 1 /project/umw_john_doe/folder 1> ~/du.out 2> ~/du.err
```
Note that there is no space between the `1` or `2` and `>` signs which is important. When used in this way `1` indicates stdout, which is typically the output of the command and `2` indicates stderr which is any errors that may arise from the command. An example of errors for this command would be directories or subdirectories that you do not have permission to view.

Inspect command output in the `du.out`:  
```bash
less ~/du.out

# 40M   /project/umw_john_doe/folder/subdir1
# 400M  /project/umw_john_doe/folder/subdir2
# 400M  /project/umw_john_doe/folder/subdir3
# ...
# 2G    /project/umw_john_doe/folder

```
`less` command displays one screenful of a text file at a time. If your document has more than one screenful text, you can scroll with your mouse or use page up and down, up and down arrrows on your keyboard to navigate. You will need to use the keyboard key <kbd>q</kbd> to exit from `less`. Typical <kbd>ctrl</kbd> + <kbd>c</kbd> used for exiting from most programs will not work.

Similarly inspect the error messages in `du.err`:
```bash
less ~/du.err

# du: cannot read directory `/project/umw_john_doe/folder/subdir8/subsubdir9': Permission denied
```

If you want to find out permission and ownership of the directory causing the error, use `stat` command:
```bash
stat -c %U:%G:%A:%n /project/umw_john_doe/folder/subdir8/subsubdir9

# userX:groupY:drwx------:/project/umw_john_doe/folder/subdir8/subsubdir9
```
The output indicates the problem directory belongs to `userX` and the permissions are `drwx` for the owner, `---` for the group and others. If you are not the userX, you will not be able to view the contents of this directory. If the permissions were `drwxr-x---` instead, you would be able to view it, assuming you are in the groupY. 



