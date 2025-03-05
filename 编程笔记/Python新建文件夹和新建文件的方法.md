```PYTHON
import os
import shutil
def RemoveDir(filepath):
    if not os.path.exists(filepath):
        os.mkdir(filepath)
    else:
        shutil.rmtree(filepath)
        os.mkdir(filepath)


def cleartxt(path):
    with open(path, 'a+') as f:
        f.truncate(0)
        f.close()
```
```python
1.    
    with open("bbb.jpg", "wb")as f: # wb是写二进制
    
2.  f.write(r.content)
```
