# What is this?

An alternative OpenGL implementation that is specifically made for Natural Selection 2.
NS2 does not use the OpenGL API correctly, and thus needs something like this.

# Benefits

Crashes less

# How do I use this?

Requirements:
You must have meson and a C compiler (e.g. GCC) installed.

It's quite simple:
You first download the project (either clone it with git or download the zip file through github).
After that you open a terminal in the project directory, and run `meson build`.
Then you must make a directory called `install` through the command `mkdir install`.
You then `cd` to that directory, and run `meson configure -Dprefix=/the/full/path/to/the/install/directory/we/just/made`.
You can also do `meson configure -Dbuildtype=release` to increase the speed of mesa, although this will increase compile times
a bit. I heavily recommend that you do this unless you're debugging a crash.

(Optional step: run `mesa configure -Dgallium-drivers=<mydriver>` to reduce build times, e.g. radeonsi for AMD cards)

You can now run `ninja` and then `ninja install`, which should build the project.

## Running NS2 with it

You must set the environment variable `LD_LIBRARY_PATH` to the absolute path to the `lib` subdir of the install directory,
and the `LIBGL_DRIVERS_PATH` to the absolute path to the `dri` subdir of the `lib` folder.

Example:
```bash
export LD_LIBRARY_PATH=$HOME/mesa-ns2/install/lib/
export LIBGL_DRIVERS_PATH $HOME/mesa-ns2/install/lib/dri/
```

After setting these environment variables, you can just run NS2.

You can e.g. put this in the launch options for NS2 in steam:
`env LD_LIBRARY_PATH=/my/install/lib/ LIBGL_DRIVERS_PATH=/my/install/lib/dri/ %command%`
which will set the environment variables before running NS2.

### WARNING
Do not do this when you are not running NS2, as it will be incompatible with a great deal of
OpenGL applications.
