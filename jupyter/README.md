# Jupyter

`/home/jupyter/notebooks` is the default folder to hold notebooks in the container, so it should be mapped to persist data.

Password can be customized by setting PWD_HASH. To get the hash for the chosen password:

```python
In [1]: from notebook.auth import passwd
In [2]: passwd()
Enter password:
Verify password:
Out[2]: 'sha1:cf3676de7ab9:35a0b327a51dcd27e4f83b5ef9545878372e7f94'
```