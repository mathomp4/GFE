# Goddard Fortran Ecosystem (GFE) SDK

This repo is intendend to be a single fixture for the [Goddard Fortran Ecosystem](https://github.com/Goddard-Fortran-Ecosystem) libraries. This is useful for superprojects that depend on the GFE libraries. It is self-sufficient and prior installations of pFUnit/fArgParse/gFTL-share/gFTL are not required to run the unit tests. 

## Current versions

| Package     | Version |
| :------     | :------ |
| gFTL        | v1.7.0  |
| gFTL-shared | v1.4.1 |
| fArgParse   | v1.2.0 |
| yaFyaml     | v1.0-beta8 |
| pFlogger    | v1.8.0 |
| pFUnit      | v4.2.5 |

## Set up

Clone the repository and update the submodules. Note that the `--recursive` flag to `git submodule update` is not required:
```console
$ git clone https://github.com/Goddard-Fortran-Ecosystem/GFE.git
$ cd GFE
$ git submodule update --init     # don't need --recursive
```

Create a build directory, and configure the build. Set `CMAKE_INSTALL_PREFIX` to a path that GFE libraries should be installed to.

```console
$ mkdir build/
$ cd build/
$ cmake .. -DCMAKE_INSTALL_PREFIX=/my/software
...
-- Configuring done
-- Generating done
-- Build files have been written to: /home/user/GFE/build
```

Compile all the GFE libraries

```console
$ make -j6
```

and lastly install (necessary for testing):

```console
$ make install
```

### Testing

The GFE libraries use the pFUnit unit testing framework. pFUnit is a GFE library itself, so to set up and run the GFE tests we need to build the tests against our installation (previous step). Point CMake to your GFE install prefix with `CMAKE_PREFIX_PATH`. Builds are enabled by setting `BUILD_TESTING` to a true boolean.

```console
$ cmake .. -DCMAKE_PREFIX_PATH=/my/software
...
-- Configuring done
-- Generating done
-- Build files have been written to: /home/user/GFE/build
```

Compile the tests:
```console
$ make -j20 tests
```

Finally, the tests can be executed like so

```console
$ ctest
ctest
Test project /home/user/GFE/build
[ 14%] Built target generate-type-incs
[ 17%] Built target generate-template-incs
[ 31%] Built target gftl-shared
[ 39%] Built target yafyaml
[ 43%] Built target fargparse
[ 43%] Built target posix_predefined.x
[ 43%] Built target generate_posix_parameters
[ 53%] Built target funit-core
[ 60%] Built target fhamcrest
[ 73%] Built target asserts
[ 73%] Built target funit-main
[ 73%] Built target funit
[ 78%] Built target yafyaml_tests.x
[ 78%] Built target other_shared
[ 87%] Built target new_tests.x
[ 92%] Built target funit_tests
[ 92%] Built target funit_tests.x
[ 92%] Built target robust
[ 95%] Built target remote.x
[ 95%] Built target robust_tests.x
[100%] Built target fhamcrest_tests.x
[100%] Built target build-tests
      Start  1: vector_tests
 1/19 Test  #1: vector_tests ...............................   Passed    0.01 sec
      Start  2: map_tests
 2/19 Test  #2: map_tests ..................................   Passed    0.01 sec
      Start  3: set_tests
 3/19 Test  #3: set_tests ..................................   Passed    0.00 sec
      Start  4: altSet_tests
 4/19 Test  #4: altSet_tests ...............................   Passed    0.00 sec
      Start  5: fargparse_tests
 5/19 Test  #5: fargparse_tests ............................   Passed    0.00 sec
      Start  6: unit_test_processor
 6/19 Test  #6: unit_test_processor ........................   Passed    0.05 sec
      Start  7: processor_test_MpiParameterizedTestCaseC
 7/19 Test  #7: processor_test_MpiParameterizedTestCaseC ...   Passed    0.07 sec
      Start  8: processor_test_MpiTestCaseB
 8/19 Test  #8: processor_test_MpiTestCaseB ................   Passed    0.07 sec
      Start  9: processor_test_ParameterizedTestCaseB
 9/19 Test  #9: processor_test_ParameterizedTestCaseB ......   Passed    0.07 sec
      Start 10: processor_test_TestA
10/19 Test #10: processor_test_TestA .......................   Passed    0.07 sec
      Start 11: processor_test_TestCaseA
11/19 Test #11: processor_test_TestCaseA ...................   Passed    0.07 sec
      Start 12: processor_test_beforeAfter
12/19 Test #12: processor_test_beforeAfter .................   Passed    0.07 sec
      Start 13: processor_test_simple
13/19 Test #13: processor_test_simple ......................   Passed    0.07 sec
      Start 14: old_tests
14/19 Test #14: old_tests ..................................   Passed    0.01 sec
      Start 15: robust_tests.x
15/19 Test #15: robust_tests.x .............................   Passed    0.00 sec
      Start 16: new_tests.x
16/19 Test #16: new_tests.x ................................   Passed    0.01 sec
      Start 17: fhamcrest_tests.x
17/19 Test #17: fhamcrest_tests.x ..........................   Passed    0.00 sec
      Start 18: yafyaml_tests.x
18/19 Test #18: yafyaml_tests.x ............................   Passed    0.01 sec
      Start 19: pflogger_tests.x
19/19 Test #19: pflogger_tests.x ...........................   Passed    0.02 sec

100% tests passed, 0 tests failed out of 19

Total Test time (real) =   0.65 sec
```
