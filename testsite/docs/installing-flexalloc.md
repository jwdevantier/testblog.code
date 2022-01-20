# Installing FlexAlloc

## Dependencies

### Package dependencies
Meson will inform you of missing C libraries, but you will at least need the following software to
build FlexAlloc:

* [xnvme](https://xnvme.io)
* `meson` and `ninja` (see below)

### The meson and ninja build system
You will need the [meson](https://mesonbuild.com) build system. The easiest way to
get the latest meson package is through [pipx](https://pipxproject.github.io/pipx/) like so:

```
# (replace 'python3' with 'python' if this is your Python 3 binary)
python3 -m pip install --user pipx
python3 -m pipx ensurepath
```

Afterward, install `meson` and `ninja` into their own virtual environment:
```
pipx install meson
pipx runpip meson install ninja
```

**NOTE** You may see errors indicating that you miss `venv` or `virtualenv`. In some Distribution,
this Python module is shipped separately. For Ubuntu/Debian you will need to install the
`python3-venv` and `python3-pip` packages.
