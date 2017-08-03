Sonar-cxx (here: [cxx-v0.9.7](https://github.com/SonarOpenCommunity/sonar-cxx/releases/tag/cxx-0.9.7)) can be installed into a [SonarQube Docker Image](https://hub.docker.com/_/sonarqube/) like follows:

    sudo docker search sonarqube
    sudo docker pull sonarqube
    sudo docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube  # runs under http://localhost:9000
    wget https://github.com/SonarOpenCommunity/sonar-cxx/releases/download/cxx-0.9.7/sonar-cxx-plugin-0.9.7.jar  # get sonar-cxx v0.9.7
    sudo docker cp ./sonar-cxx-plugin-0.9.7.jar sonarqube:/opt/sonarqube/extensions/plugins/sonar-cxx-plugin-0.9.7.jar  # install plugin into plugin directory
    sudo docker restart sonarqube