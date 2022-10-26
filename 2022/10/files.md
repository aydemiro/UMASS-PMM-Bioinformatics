### File system disk usage analysis with df
Read the manual of du command with ```man df```  
Use ```df``` command to see the disk usage at file system level. This is useful to learn how much space is used/available in a given mount point. Example mount points are:  
1) Your groups project space
2) Your home space
3) Your groups nearline space

Use with ```-h``` option for human readable values (GB, MB, etc)

Example:
```bash
df -h /project/umw_ozkan_aydemir
```
### Disk usage analysis with du
Read the manual of du command with ```man du```  
Use ``du`` command to estimate disk usage of a given directory and its subdirectories. This is useful when you want to know how much space a certain directory is taking up.  
Use with ```-h``` option for human readable values (GB, MB, etc).

Example:

Find disk usage in ```/project/umw_ozkan_aydemir/dev```
```bash
du -h /project/umw_ozkan_aydemir/dev
```
Find disk usage in ```/project/umw_ozkan_aydemir/dev``` without listing its subdirectories. ```-s``` option skips the subdirectories.
```bash
du -h -s /project/umw_ozkan_aydemir/dev
```
Find disk usage in ```/project/umw_ozkan_aydemir/dev``` and its first level subdirectories.
```bash
du -h --max-depth 1 /project/umw_ozkan_aydemir/dev
```
