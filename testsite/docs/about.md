# About about..


```c
struct linereader
{
  FILE *fp;
  char *buf;
  unsigned int buf_len;
};
```

```python
def md_open(dev_uri: str, md_dev_uri: str) -> FlexAlloc:
    dev_pystr = dev_uri.encode("ascii")
    cdef char *dev_cstr = dev_pystr
    md_dev_pystr = md_dev_uri.encode("ascii")
    cdef char *md_dev_cstr = md_dev_pystr

    cdef flexalloc *data
    if fla_md_open(dev_cstr, md_dev_cstr, &data):
        raise MemoryError("failed to open FlexAlloc system")

    cdef FlexAlloc fs = FlexAlloc.from_ptr(data)
    return fs
```