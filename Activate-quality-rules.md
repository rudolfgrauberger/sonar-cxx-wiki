# Activate quality rules
## Terminology

Similar to other SonarQube plugins, sonar-cxx implements an internal analyzer aka **sensor** called "SquidSensor". Importing functionality for [external tools](https://github.com/SonarOpenCommunity/sonar-cxx/wiki/Running-tools) is also implemented with corresponding sensors. 

Each type of warning, which can be issued by a sensor is represented by a **quality rule**. Rules are grouped into **rules repositories**, whereby there is 1:1 relationship between a sonar-cxx sensor and the rule repository. E.g. sonar-cxx installs the following repositories:

* PC-lint
* Compiler-VC
* Cppcheck
* RATS
* Compiler-GCC
* Clang-Tidy
* Clang-SA
* Vera++
* Valgrind
* c++ SonarQube (SquidSensor)

All rules (and rules repositories) for some particular language are grouped into **quality profiles**. E.g. for the language "C++ (Community)" sonar-cxx installs the default quality profile called "Sonar way".

## Activation of quality rules

The total number of all rules in the sonar-cxx's quality profile "C++ (Community) Sonar way" is very high (~ 4k rules). Enabling all of them would have a negative effect on analysis performance. For this reason all rules (rules repositories) are disabled by default. This fact disables all sensors, too.

In order to enable some sensor(s), administrator have to initially activate corresponding quality rules (rules repositories). 

1. The default quality profile "C++ (Community) Sonar way" is read only. Therefore please create a copy of the default "Sonar way" profile ([http://sonarserver/profiles](http://sonarserver/profiles) -> C++ (Community) -> SonarWay -> gear-wheel -> Copy -> name your custom profile e.g. like "ProjectName Way")

2. Afterwards activate relevant rules in "ProjectName Way" profile ([http://sonarserver/coding_rules](http://sonarserver/coding_rules) -> QualityProfiles -> Choose "ProjectName Way" -> Choose "inactive" on the same line -> Repositories -> Choose the desired sensor -> [bulk] activate rules you are interested in
