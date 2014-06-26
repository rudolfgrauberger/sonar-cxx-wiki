_The C++ Community plugin wont execute neither test runners not coverage tracers nor static checkers itself. All this data has to be provided in form of reports. See [[Running tools]]._

### Usage

You can analyze your projects using the usual means (see [this](http://www.sonarqube.org/at-long-last-sonarqube-is-a-true-polyglot/) page for all available). All runners should work. See below for details.

### The usual setup

Analysis of a C++ project involves usually three steps:

1. Run the tools (see [[Running tools]]) which are of interest for you and store the results in a file somewhere underneath the root directory of your project. Its usually convenient to put this into the build system; a shell script may be a good choice, too.

2. Provide a configuration using the file "sonar-project.properties". Set following properties, besides the standard ones:
   - **sonar.language** to "c++". This is required for SonarQube's < 4.2. For SonarQube's >= 4.2, leaving this property unset enables the [multi-language feature](http://www.sonarqube.org/at-long-last-sonarqube-is-a-true-polyglot/).
   - Optional: **sonar.cxx.includeDirectories** and **sonar.cxx.defines** (see [[Supported configuration properties]])
   - Optional: paths to the generated reports (see [[Supported configuration properties]])

3. Make sure the SonarQube Server is running
4. Use the SonarQube runner to start the analysis and feed the data into SonarQube. This usualy boils down to calling the runner in the root directory of your project:
```BASH
$ cd <project root>
$ sonar-runner
```

There may be a Step '0' too: "_use your build system to make a build suitable for running the Step 1_". This may be the case for collecting coverage statistics when using gcc+gcov, for example.

For details how to invoke the tools and tie it all together see the [sample project](https://github.com/wenns/sonar-cxx/tree/master/sonar-cxx-plugin/src/samples/SampleProject2).

### Maven projects

There is a maven plugin which automates running of a sonar analysis on a C++ project but requires a maven setup. Running a SonarQube analysis on maven projects is quite simple and usually a matter of:

1. Getting and installing the [cxx-maven-plugin](https://github.com/franckbonin/cxx-maven-plugin) ([usage](https://github.com/franckbonin/cxx-maven-plugin/wiki/Introduction)). If you use multiple source directories and depend on cxx:addsource goal, you shall use -Dsonar.phase=cxx:addsource option (see [Sonar Maven Plugin Project Configuration](http://docs.codehaus.org/display/SONAR/Analysis+Parameters) )

2. Setting the language property and the source directory in your pom:
``` 
  <properties>
    ...
    <sonar.language>c++</sonar.language>
    ...
  </properties>
 
  <build>
    ...
    <sourceDirectory> path </sourceDirectory>
    ...
  </build>
```
3. Make sure your SonarQube server is running.

4. Start the analysis with
```bash
$ mvn sonar:sonar
```
or
```bash
$ mvn sonar:sonar -Dsonar.phase=cxx:addsource
```


For details see the [sample maven project](https://github.com/wenns/sonar-cxx/tree/master/sonar-cxx-plugin/src/samples/SampleProject).