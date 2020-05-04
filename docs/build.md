# Overview of the build system
The COVID-19 CovidSim model uses the [CMake](www.cmake.org) build tool to generate build files for other build systems. Currently, building using clang and gcc with Makefiles and MSVC with Visual Studio are supported.

# Building with Makefiles
From the command line inside a git clone, run the following:
```
mkdir build
cd build
cmake ../src
make
```
# Building with Visual Studio project files from Cmake
From the command line inside a git clone, run the following:
```
mkdir build
cd build
cmake ../src
```
This will create project files inside the `build` directory that can be opened in Visual Studio. Modifications to the CMake configuration may require regenerating the Visual Studio projects.

# Building directly with CMake in Visual Studio 2019
Visual Studio 2019 supports using CMake to manage the build directly by selecting File -> Open -> Cmake... and opening `src/CMakeLists.txt`. Then Visual Studio's normal build shortcuts will update the CMake configuration as well as building the project.

CMake options are configured using the `CMakeSettings.json` file, which Visual Studio will generate when `CMakeLists.txt` is opened. If a python3 interpreter is not available in your PATH, you may wish to either disable regression tests (they are enabled by default), or provide the path to a valid python3 interpreter.

# Build options
Additional configuration variables can be provided in the `cmake` invocation.

- `USE_OPENMP` determines whether the model is compiled with parallelization using OpenMP. This option defaults to on, but can be disabled by passing `-DUSE_OPENMP=OFF`. The simulation is designed to be run on multi-core systems. Performance improvements are approximately linear up to 24 to 32 cores, depending on memory performance.
- `ENABLE_REGRESSION_TEST` enables running the regression tests via ctest, which requires a working python3 interpreter to be available. A python interpreter can be specified by passing `-DPYTHON_EXECUTABLE:FILEPATH=<PATH_TO_PYTHON>`. Regression tests can be disabled by passing `-DENABLE_REGRESSION_TEST:BOOL=OFF`. By default, regression tests are enabled, and can be invoked by simply running `make test` or running `ctest` on the command-line manually.

For Makefile builds, a build type can be specified by passing `-DCMAKE_BUILD_TYPE=Debug`, `-DCMAKE_BUILD_TYPE=MinSizeRel`, `-DCMAKE_BUILD_TYPE=Release`, or `-DCMAKE_BUILD_TYPE=RelWithDebInfo`. By default, Makefile builds will use `RelWithDebInfo`.

# VisualStudio solution
A manually created VS-2019 solution and project is included for convenience, but it should not be considered the source of truth for the project.
