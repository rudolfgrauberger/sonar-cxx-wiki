The plugin contains a small but growing
[integration test suite](https://github.com/wenns/sonar-cxx/tree/master/sonar-cxx-plugin/src/test/integration).
It provides a means to check that the plugin works (or works not) with a
particular SonarQube version/setup.


## Preconditions

Make sure the following preconditions are met, before running the test suite:

* Python is installed
* behave (http://pythonhosted.org/behave/) is installed
* [request module](https://pypi.python.org/pypi/requests) is available ('pip install requests' may help)
* Optional: [colorama module](https://pypi.python.org/pypi/colorama/0.3.2) is installed ('pip install colorama')


## Usage
Either install the plugin, startup SonarQube manually and simply run:

```BASH
$ behave
```

from the project root folder or let the test suite do the job by
telling it the path to your SQ installation:

```BASH
$ SONARHOME=/path/to/SonarQube behave
```

In the latter case, the suite will automatically install and test the
jar in sonar-python-plugin/target. So make sure the plugin is build
and the jar is available.
