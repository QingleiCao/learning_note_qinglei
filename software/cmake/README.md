# Routines
## find_path
```
find_path (<VAR> name1 [path1 path2 ...])
```
This command is used to find a directory containing the named file. A cache entry, or a normal variable if NO_CACHE is specified, named by <VAR> is created to store the result of this command. If the file in a directory is found the result is stored in the variable and the search will not be repeated unless the variable is cleared. If nothing is found, the result will be <VAR>-NOTFOUND.

```
find_path(SDE_INCLUDE_DIR sde_lib.h
          PATHS ${PAPI_ROOT}/include ENV PAPI_INCLUDE_DIR
          DOC "Include path for PAPI SDE")
```

## find_library
find_library (<VAR> name1 [path1 path2 ...])

https://cmake.org/cmake/help/v3.0/command/find_library.html

```
find_library(SDE_LIBRARY NAMES sde
             HINTS ${PAPI_ROOT}/lib ENV PAPI_LIBRARY_DIR
             DOC "Library path for PAPI SDE")
```

## find_package_handle_standard_args
This command handles the REQUIRED, QUIET and version-related arguments of find_package(). It also sets the <PackageName>_FOUND variable. The package is considered found if all variables listed contain valid results, e.g. valid filepaths.
```
include(FindPackageHandleStandardArgs)
find_package_handle_standard_args(SDE DEFAULT_MSG
                                  SDE_LIBRARY SDE_INCLUDE_DIR )
```

## TARGET

```
    if(NOT TARGET PAPI::SDE)
      add_library(PAPI::SDE INTERFACE IMPORTED)
    endif()

    set_property(TARGET PAPI::SDE APPEND PROPERTY INTERFACE_LINK_LIBRARIES "${SDE_LIBRARY}")
    set_property(TARGET PAPI::SDE PROPERTY INTERFACE_INCLUDE_DIRECTORIES "${SDE_INCLUDE_DIR}")
```

## mark_as_advanced
```
mark_as_advanced([CLEAR|FORCE] <var1> ...)
```

Sets the advanced/non-advanced state of the named cached variables.

An advanced variable will not be displayed in any of the cmake GUIs unless the show advanced option is on. In script mode, the advanced/non-advanced state has no effect.

If the keyword CLEAR is given then advanced variables are changed back to unadvanced. If the keyword FORCE is given then the variables are made advanced. If neither FORCE nor CLEAR is specified, new values will be marked as advanced, but if a variable already has an advanced/non-advanced state, it will not be changed.

Changed in version 3.17: Variables passed to this command which are not already in the cache are ignored. See policy CMP0102.

```
  set(SDE_LIBRARIES ${SDE_LIBRARY} )
  set(SDE_INCLUDE_DIRS ${SDE_INCLUDE_DIR} )
  mark_as_advanced(FORCE SDE_INCLUDE_DIR SDE_LIBRARY)
```

Another example:
This will not replace an existing value. This is so that you can set these on the command line and not have them overridden when the CMake file executes. If you want to use these variables as a make-shift global variable, then you can do:
```
set(MY_CACHE_VARIABLE "VALUE" CACHE STRING "" FORCE)
mark_as_advanced(MY_CACHE_VARIABLE)
```

## Variables and the Cache

https://cliutils.gitlab.io/modern-cmake/chapters/basics/variables.html
