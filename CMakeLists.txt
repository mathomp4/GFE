cmake_minimum_required(VERSION 3.12)
project (GFE
  VERSION 1.0.0
  LANGUAGES Fortran
)
cmake_policy(SET CMP0074 NEW)

enable_testing()

add_subdirectory(gFTL)
add_subdirectory(gFTL-shared)
add_subdirectory(fArgParse)
add_subdirectory(pFUnit)
add_subdirectory(yaFyaml)
add_subdirectory(pFlogger)
