# SA-MP Plugin SDK

This is a copy of the SA-MP plugin SDK files extracted from MapAndreas (a plugin by Kalcor). It is the bare minium that you need to develop plugins. 

The plugin SDK used to be hosted on the SA-MP website but was removed for some reason, hence this repo was born. 

## About this fork
CMake support was added to improve the library usability. No library code
changes are intended, but feel free to submit pull requests about the CMake
part.

### Installation (on Windows should be ran with admin privileges):
```
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build
cmake --install build
```

### Usage:
```cmake
find_package(sampsdk REQUIRED)

target_link_libraries(myapp PRIVATE sampsdk::sampsdk)
```

---

Also `SAMPSDK_INCLUDE_DIR` is defined by library config after you call
`find_package`. You probably won't need it (include directory is set by means
of `sampsdk::sampsdk` target) but anyway just know that such variable exists.
