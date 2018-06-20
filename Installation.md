- Make sure you know which plug-in release is compatible with your SonarQube instance (see [[SonarQube compatibility matrix]])
- download one of the [released](https://github.com/wenns/sonar-cxx/releases) jar packages into the SONARQUBE_HOME/extensions/plugins directory
   - `sonar-cxx-plugin-x.y.z.jar`: is the c++ plug-in
   - `sonar-c-plugin-x.y.z.jar`: is the c plug-in
- restart the SonarQube server
- Navigate to the _Update Center_ (\<Your SonarQube URL\>/Administration/System/Update Center). The _Update Center_ should list 'C++ (Community)' on the tab 'Installed'.

Additional tools:
   - `sslr-cxx-toolkit-x.y.z.jar`: Is an additional tool to create an AST from source code. Helpful to create XPath checks. This is not a plug-in. Don't copy it into the _plugins_ folder.
