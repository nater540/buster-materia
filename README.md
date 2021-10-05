# Buster Materia Firmware

```shell
ESPPORT=/dev/cu.usbserial-0001
ESPBAUD=115200
ninja flash -C build
```


Type `idf.py --help` for a list of commands. Here are a summary of the most useful ones:

`idf.py set-target <target>` sets the target (chip) for which the project is built. See Selecting the Target.

`idf.py menuconfig` runs the “menuconfig” tool to configure the project.

`idf.py build` will build the project found in the current directory. This can involve multiple steps:

Create the build directory if needed. The sub-directory build is used to hold build output, although this can be changed with the -B option.

Run CMake as necessary to configure the project and generate build files for the main build tool.

Run the main build tool (Ninja or GNU Make). By default, the build tool is automatically detected but it can be explicitly set by passing the -G option to idf.py.

Building is incremental so if no source files or configuration has changed since the last build, nothing will be done.

`idf.py clean` will “clean” the project by deleting build output files from the build directory, forcing a “full rebuild” the next time the project is built. Cleaning doesn’t delete CMake configuration output and some other files.

`idf.py fullclean` will delete the entire “build” directory contents. This includes all CMake configuration output. The next time the project is built, CMake will configure it from scratch. Note that this option recursively deletes all files in the build directory, so use with care. Project configuration is not deleted.

`idf.py flash` will automatically build the project if necessary, and then flash it to the target. The -p and -b options can be used to set serial port name and flasher baud rate, respectively.

`idf.py monitor` will display serial output from the target. The -p option can be used to set the serial port name. Type Ctrl-] to exit the monitor. See IDF Monitor for more details about using the monitor.

`idf.py app`, `idf.py bootloader`, `idf.py partition_table` can be used to build only the app, bootloader, or partition table from the project as applicable.

There are matching commands `idf.py app-flash`, etc. to flash only that single part of the project to the target.

`idf.py -p PORT erase_flash` will use esptool.py to erase the target’s entire flash chip.

`idf.py size` prints some size information about the app. size-components and size-files are similar commands which print more detailed per-component or per-source-file information, respectively. If you define variable -DOUTPUT_JSON=1 when running CMake (or idf.py), the output will be formatted as JSON not as human readable text. See idf.py-size for more information.

`idf.py reconfigure` re-runs CMake even if it doesn’t seem to need re-running. This isn’t necessary during normal usage, but can be useful after adding/removing files from the source tree, or when modifying CMake cache variables. For example, idf.py -DNAME='VALUE' reconfigure can be used to set variable NAME in CMake cache to value VALUE.

`idf.py python-clean` deletes generated Python byte code from the IDF directory which may cause issues when switching between IDF and Python versions. It is advised to run this target after switching versions of Python.

`idf.py docs` will open direct link to documentation for project’s chip target and version in browser. To see all options use `idf.py docs --help`
