###Sign up for GitHub

TBD

###Checkout Sources

If you have never used Git before, you need to do some setup first. Run the following commands so that GIT knows your name and email.
```
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```
Setup line endings preferences:
```
# For Unix/Mac users
git config --global core.autocrlf input
git config --global core.safecrlf true

# For Windows users
git config --global core.autocrlf true
git config --global core.safecrlf true
```
Get sources by executing:
```
git clone https://github.com/wenns/sonar-cxx.git
```

Committers must configure their SSH key (see GitHub documentation for Windows and Mac) and clone repository:
```
git clone git@github.com:wenns/sonar-cxx.git
```

###Build
* Install JDK 7 or greater.
* Install Maven 3.2.1 or greater.
* Execute ```mvn clean install``` on command line in root folder of your local copy.
* For development you can use e.g. Eclipse or NetBeans 8.0 or greater.

###Debug

If you want to debug your code there are at least three possibilities:

1. Best and easiest possibility is to write an Unit Test for your changes. In this case you can run your debugger for your particular Unit Test to debug into your code within the IDE. Any other changes are not needed in this case.
2. In case you have to **debug code which is executed during analyzer run** you have to prepare and start the sonar-runner for debugging.
 1. Copy your plugin's jar file to ```SONAR_HOME/extensions/plugins```
 2. Start SonarQube normally, (debug is commented out in wrapper.config)
 3. At a command prompt, cd to the directory of the project you'll be analyzing
 4. Start sonar-runner in debug mode with the following commands<br>```SET SONAR_RUNNER_OPTS=-Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address=8000```
 5. Attach the IDE to the debug process on port 8000, set breakpoints in the source, and debug!
3. In case you have to **debug code on the sever side** do the following steps:
 1. Copy your plugin's jar file to ```SONAR_HOME/extensions/plugins```
 2. Edit ```SONAR_HOME/conf/wrapper.conf``` and uncomment the line: ```wrapper.java.additional.3=-agentlib:jdwp=transport=dt_socket,server=y,address=8000```
 3. Launch SonarQube normally. The following line will appear in the log: Listening for transport dt_socket at address: 8000
 4. Attach the IDE to the debug process on port 8000, set breakpoints in the source, and debug!

See also [Coding a Plugin / Debugging](http://docs.codehaus.org/display/SONAR/Debugging)

###Testing

We have plenty of unit tests (not all of them being really 'unit')  and a couple of integration-level smoke-tests.
The former can be run with e.g. ```mvn test```; refer to [[Integration test suite]] on how to use the latter.

###Helpful Links
* [Extension Guide](http://docs.codehaus.org/display/SONAR/Extension+Guide)
* [Developing Plugins](http://docs.codehaus.org/display/SONAR/Developing+Plugins)
* [Coding a Plugin](http://docs.codehaus.org/plugins/servlet/mobile#content/view/129565136)
* [API Changes](http://docs.codehaus.org/display/SONAR/API+Changes)
