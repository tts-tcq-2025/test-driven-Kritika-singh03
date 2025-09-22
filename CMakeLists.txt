# Set test source file
set(TEST_SRC "tests/test_StringCalculator.cpp")

# Unit test target (only add if the file exists)
if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/${TEST_SRC}")
    add_executable(test-monitor ${TEST_SRC})
    
    # Link test executable with GoogleTest + StringCalculator
    target_link_libraries(
        test-monitor
        PRIVATE
        StringCalculator
        GTest::gtest_main
    )

    # Test discovery
    include(GoogleTest)
    gtest_discover_tests(test-monitor)
else()
    message(WARNING "Test source file '${TEST_SRC}' not found. Skipping test-monitor target.")
endif()
