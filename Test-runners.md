### Googletest
Googletest is a C++ testing framework written by Google. To create JUnitReport compatible output call it this way:
```BASH
<test executable> --gtest_output=xml:<filename>
```

### Boost Test Library

The [Boost Test Library](http://www.boost.org/doc/libs/release/libs/test) provides a matched set of components for writing test programs, organizing tests in to simple test cases and test suites, and controlling their runtime execution. For a more detailed parameter description see [Runtime parameters reference](http://www.boost.org/doc/libs/release/libs/test/doc/html/utf/user-guide/runtime-config/reference.html). To create JUnitReport compatible output call it this way:

```BASH
<test executable> --log_format=XML --log_sink=<filename> --log_level=all --report_level=no
```

Resulting report using BOOST_TEST_MODULE, BOOST_AUTO_TEST_SUITE and BOOST_AUTO_TEST_CASE:

```XML
<?xml version="1.0" ?>
<TestLog>
  <!-- BOOST_TEST_MODULE -->
  <TestSuite name="BoostTestModuleName">
    <!-- BOOST_AUTO_TEST_SUITE -->
    <TestSuite name="BoostTestSuiteName">
      <!--  BOOST_AUTO_TEST_CASE -->
      <TestCase name="BoostTestCaseName">
        <!--BOOST_CHECK_XXX -->
        <Info file="./base.test.boost/exceptiontest.cpp" line="21"><![CDATA[check 'incorrect exception Exception is caught' passed]]></Info>
        <!--BOOST_CHECK_XXX -->
        <Info file="./base.test.boost/exceptiontest.cpp" line="23"><![CDATA[check 'incorrect exception LocalException is caught' passed]]></Info>
        <TestingTime>2000</TestingTime>
      </TestCase>
    </TestSuite>
  </TestSuite>
</TestLog>
```
