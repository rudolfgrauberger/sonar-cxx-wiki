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

TBD

###Testing

TBD

###Helpful Links
* [Extension Guide](http://docs.codehaus.org/display/SONAR/Extension+Guide)
* [Developing Plugins](http://docs.codehaus.org/display/SONAR/Developing+Plugins)
* [API Changes](http://docs.codehaus.org/display/SONAR/API+Changes)
