# Usage

You can analyze your projects using the usual means (see [this](http://docs.codehaus.org/display/SONAR/Installing+and+Configuring+Sonar+Runner) page for all available). All runners should work. See below for details.

# The usual setup

Analysis of a c++ project involves usually three steps:

1. Run the tools (see Running tools) which are of interest for you and store the results in a file somewhere underneath the root directory of your project. Its usually convenient to put this into the build system; a shell script may be a good choice, too.

2. Provide a configuration using the file "sonar-project.properties". Set following properties, besides the standard ones:

- Required: sonar.language to "c++".

- Optional: sonar.cxx.include_directories and sonar.cxx.defines (see [[Configuration]])

- Optional: paths to the generated reports (see [[Configuration]])

3. Use the SonarQube runner  to start the analysis and feed the data into SonarQube.

There may be a Step '0' too: "use your build system to make a build suitable for running the Step 1". This may be the case for collecting coverage statistics when using gcc+gcov, for example.

For details how to invoke the tools and tie it all together see the sample project.