# What is this?

An alternative OpenGL implementation that is specifically made for Natural Selection 2.
NS2 does not use the OpenGL API correctly, and thus needs something like this.

# Benefits

Crashes much less

# How do I use this?

Requirements:
You must have meson and a C compiler (e.g. GCC) installed.

It's quite simple:
You first download the project (either clone it with git or download the zip file through github).

After downloading the project, you must open a terminal within the root directory
of the project.

You must now create your installation directory by e.g. running `$ mkdir install`.
You must also create a build directory by running `$ meson build`.
After creating your build directory, you must `$ cd` to it to set it up.

First, you must specify the installation directory (known as prefix path), by running the following command:
`$ meson configure -Dprefix=$INSTALL_DIR`, but replace `$INSTALL_DIR` with
the **full and absolute** path to the `install` directory you just created.

If you wish to give the performance of this OpenGL implementation a nice boost,
you can run the command `$ meson configure -Dbuildtype=release`, which will
enable some extra optimizations and strip the build of a lot of debugging information,
which will also heavily reduce the size of the resulting binaries.

Another optional step which reduces the time to compile this OpenGL implementation, and also
reduce the size of the binaries, is to run the following command: `$ mesa configure -Dgallium-drivers=$MYDRIVERS`,
where you replace `$MYDRIVERS` with whatever drivers you require.
For GCN (7000 and later) AMD cards this is `radeonsi`.

You are now ready to compile the project, and to do that you must run the command `$ ninja install`.

## Running NS2 with it

You must set the environment variable `LD_LIBRARY_PATH` to the absolute path to
the `lib` subdirectory within the installation directory you specified.

You must then set the environment variable `LIBGL_DRIVERS_PATH` to the absolute path
to the `dri` subdirectory within the `lib` subdirectory mentioned above.

Example:
```bash
$ export LD_LIBRARY_PATH=$HOME/mesa-ns2/install/lib/
$ export LIBGL_DRIVERS_PATH $HOME/mesa-ns2/install/lib/dri/
```

To set these environment variables automatically before running NS2 through steam,
you can set these within the launch options for NS2, which you access through the properties
menu by right-clicking on the game within the library.
Just put this in the launch options:
`$ env LD_LIBRARY_PATH=$LIB LIBGL_DRIVERS_PATH=$DRI %command%`
where you replace `$LIB` and `$DRI` with the actual full and absolute paths to
the `lib` and `dri` subdirectories of your installation directory.

After doing this, you are ready to go!
Just launch the game through steam, if you set it up through the launch options,
or set up some script to do it for you.


### WARNING
Do not do this when you are not running NS2, as it will be incompatible with a great deal of
OpenGL applications.
