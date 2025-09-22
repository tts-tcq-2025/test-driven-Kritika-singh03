cmake_minimum_required(VERSION 3.14)
project(bms-monitor LANGUAGES CXX)

# C++17 standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# -------------------------------
# GoogleTest Setup
# -------------------------------
include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip
)

# For Windows: Prevent overriding parent project compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

FetchContent_MakeAvailable(googletest)

enable_testing()

# -------------------------------
# Sources
# -------------------------------
# Library target for StringCalculator (can be reused elsewhere)
add_library(StringCalculator
    StringCalculator.cpp
    StringCalculator.h
)

# Unit test target
add_executable(test-monitor
    tests/test_StringCalculator.cpp
)

# Link test executable with GoogleTest + StringCalculator
target_link_libraries(
    test-monitor
    PRIVATE
    StringCalculator
    GTest::gtest_main
)

# -------------------------------
# Test discovery
# -------------------------------
include(GoogleTest)
gtest_discover_tests(test-monitor)

