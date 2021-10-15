# Python Solutions

## Find .git folder list and remove

```python
#!/usr/bin/python3.9

import os
# find
# find ./code -name .git  -d

def find_folder(path,folder_name):
    folder = os.popen("find {} -name {} -depth".format(path,folder_name))
    return folder.readlines()

# arg1 is path
# arg2 is folder need to find
list = find_folder('/home/alen/code', '*.downloding')
print(list)

def remove_folder():
    
    ls = list
    for i in ls:
        os.system("rm -rf {}".format(i))

#run to remove file
#remove_folder()
def ls():
    ls = os.popen("pwd")
    # print(ls.read())
    print(ls.readlines())

# ls()

```

