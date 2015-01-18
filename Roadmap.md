The Roadmap for development of this SonarQube plugin is roughly as follows:

## 0.9.3 Release

Should be ready by the end of 05.2015.

We try to fullfil following goals:

- Rework the support of various C++ extensions and C
- Proceed in getting more C++11 syntax parsed
- Port the plugin to the API of SQ LTS
- Extend the BDD test suite, use it to detect regressions with new SQ versions early
- Fix (most of) known bugs
- Develop a strategy how to deal with future SSLR versions,
  which would lack support for preprocessing

The according milestone is:

https://github.com/wenns/sonar-cxx/issues?q=is%3Aopen+is%3Aissue+milestone%3A%22M+0.9.3%22


## Future Releases

Other major topics:

- Compatibility with other plugins in Sonar-Space (like the Issues plugin)
- lexerless parser (??)

We should strive to release every 3-4 months. As soon as we are 100%
compliant, we release the version 1.0.

To reach standard compliance, we have to address (at least) following
issues:
- Support for user-defined literals (Section 2.14.8)
- Support trigraphs
- Issue #49

A good benchmark for testing is parsing of Boost.
