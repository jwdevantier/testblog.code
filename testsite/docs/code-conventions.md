# Code Conventions:

## Code Formating
All coding style like for example positions of brackets and line break and
where to put the next line ... will be handled by calling the astyle script
located in scripts.

## Line Length
It will be 100 characters long. Enforced by running the astyle script.

## Method Signatures

### Return Value
** Always return int as error.**
In general methods should return an int where zero means that no errors occured
and any other value means an error.  If errno is detected or set within the
function it should be returned as -errno If an error different from what errno
defines is detected or set it should be returned as a positive number. This in
order to know if it is errno or a flexalloc specific error.

** Return void when there are no errors to handle.**
Use void when there are no errors to handle within the method. This is quite
rare but happens when you for example wrap a simple free.


### Initializing structures
** Pass what you are initializing to the function as a double pointer. **
In general methods should have a double pointer to the structure that is being
initialized. For example:

```c
fla_cool_function_name(int arg1, int arg2, struct fla_struct ** s)
```

## Naming

### Function naming
** Prefix "fla_". **
In general, functions that might involve a name clash must start with "fla_".
This includes API functions.

### Variable naming
** Prefix "fla_". **

### Structure alignment
** `pahole` must not show holes in structures **

### Test naming
In general there are two types of tests: 1. Unit tests (UT) and 2. Regression
tests (RT). A UT tests specific functions, it can have minimal setup but should
generaly be simple calls to self contained functions. RT on the other hand,
test features like being able to mount a FS or being able to write to
a block. These are run to make sure that current code does not introduce
regressions. when creating a regression tests you should include "_rt_" in the
name, in the same way include "_ut_" when creating unit tests.

## Error handling
For every error encountered the `flexalloc_ERR_*` methods should be used. These will
print an error message to stderr and set the appropriate return value.
Using these macros allows us to control the message format and how these get
output.

## Error reporting

Regular execution of libflexalloc should NOT output anything to std*.  Only when there is an
error should the stderr be used. This is true only when flexalloc_VERBOSITY is set to 0.

Where desired, use the `flexalloc_DBG_*` macros. The output will then be shown when
FlexAlloc is compiled with debugging enabled, such as the unit- and regression tests.

## Feature Test Macros
Feature test macros allow the porgrammer to control the definitions that are exposed when including
a header. As these might not be available in all environments, we choose to avoid them in flexalloc.

## Compile Options
### How to use them?
To set the options you can either do it at setup or configure time. In both cases you need
to add the -Doption=value to the command line in order to set the value.

### Options
  * flexalloc_VERBOSITY is an int options that can either be 0 or 1. 0 will show no extra output.
    1 means that messages called with flexalloc_VBS_PRINTF will be shown. It is set at 0 by default.