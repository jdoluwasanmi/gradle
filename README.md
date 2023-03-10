# gradle

grap a gradle index link : https://distfiles.macports.org/gradle/
cd /opt
wget https://distfiles.macports.org/gradle/gradle-6.8.3-bin.zip
unzip 
export PATH=$PATH:/opt/gradle*/bin

Install git and clone gradle from github - git clone https://github.com/Shikhar82/springboot-tomcat-gradle-war.git
go to your repo - vi build.gradle
add this syntax for sonar 
sonarqube {
    properties {
        property "sonar.sourceEncoding", "UTF-8"
                property "sonar.projectName", "springboot-tomcat-gradle-war"
                property "sonar.host.url", "http://192.168.0.59:9000"
                property "sonar.login", "94ad024cf9f892ce57c967100b4e33bd768a8d4d"
    }
}

