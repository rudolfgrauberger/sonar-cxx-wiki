The Roadmap for development of this SonarQube plugin is roughly as follows:

## 0.9.1 Release
Should be ready by somewhere around 05.2014.
It focuses on ease of use, the parsing error recovery being the core feature for that.
Besides that, there will be an assortment of new checks, support for new Sonar versions and a couple of bug fixes. This milestone includes the issues which go in: 
https://github.com/wenns/sonar-cxx/issues?milestone=2&page=1&state=open

## 0.9.X Releases
Releases after the 0.9.1 should focus getting all of c++ parsed. Other topics to address include:
- Improving the performance
- Compatibility with other plugins in Sonar-Space (like the Issues plugin)
- lexerless parser

We should strive to release every 3-4 months. As soon as we are 100% compliant, we release the version 1.0.

To reach standard compliance, we have to address (at least) following issues
- Support for user-defined literals (Section 2.14.8) 
- Support trigraphs
- Issue #47
- Issue #49

A good benchmark for testing is parsing of Boost.