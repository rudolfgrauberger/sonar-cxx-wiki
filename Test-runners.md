### Googletest
Googletest is a C++ testing framework written by Google. To create XUnit compatible output use it this way:
```BASH
<test executable> --gtest_output=xml:<filename>
```

### Boost Test Library

The [Boost Test Library](http://www.boost.org/doc/libs/release/libs/test) provides a matched set of components for writing test programs, organizing tests in to simple test cases and test suites, and controlling their runtime execution. For a more detailed parameter description see [Runtime parameters reference](http://www.boost.org/doc/libs/release/libs/test/doc/html/utf/user-guide/runtime-config/reference.html). To create XUnit compatible output use it this way:

Example:
```C++
#define BOOST_TEST_MODULE my_module
#include <boost/test/unit_test.hpp>

int add(int i, int j) { return i + j; }

BOOST_AUTO_TEST_SUITE(my_test_suite)

BOOST_AUTO_TEST_CASE(my_test)
{
	// seven ways to detect and report the same error:
	BOOST_CHECK(add(2, 2) == 4);         // #1 continues on error

	BOOST_REQUIRE(add(2, 2) == 4);       // #2 throws on error

	if (add(2, 2) != 4)
		BOOST_ERROR("Ouch...");          // #3 continues on error

	if (add(2, 2) != 4)
		BOOST_FAIL("Ouch...");           // #4 throws on error

	if (add(2, 2) != 4) throw "Ouch..."; // #5 throws on error

	BOOST_CHECK_MESSAGE(add(2, 2) == 4,  // #6 continues on error
		"add(..) result: " << add(2, 2));

	BOOST_CHECK_EQUAL(add(2, 2), 4);	 // #7 continues on error
}

BOOST_AUTO_TEST_SUITE_END()
```
Preferred command line execution to get all information (```--log_level=all``` or ```--log_level=success```):
```BASH
<test executable> --log_format=XML --log_sink=<filename> --log_level=all --report_level=no
```
Resulting Unit Test XML report:
```XML
<TestLog>
  <TestSuite name="my_module">
    <TestSuite name="my_test_suite">
      <TestCase name="my_test">
        <Info file="d:/test/example.cpp" line="11"><![CDATA[check add(2, 2) == 4 passed]]></Info>
        <Info file="d:/test/example.cpp" line="13"><![CDATA[check add(2, 2) == 4 passed]]></Info>
        <Info file="d:/test/example.cpp" line="23"><![CDATA[check 'add(..) result: 4' passed]]></Info>
        <Info file="d:/test/example.cpp" line="26"><![CDATA[check add(2, 2) == 4 passed]]></Info>
        <TestingTime>1000</TestingTime>
      </TestCase>
    </TestSuite>
  </TestSuite>
</TestLog>
```
Alternative command line to get only testsuite information (```--log_level=test_suite```):
```BASH
<test executable> --log_format=XML --log_sink=<filename> --log_level=test_suite --report_level=no
```
Resulting Unit Test XML report:
```XML
<TestLog>
  <TestSuite name="my_module">
    <TestSuite name="my_test_suite">
      <TestCase name="my_test">
        <TestingTime>1000</TestingTime>
      </TestCase>
    </TestSuite>
  </TestSuite>
</TestLog>
```
