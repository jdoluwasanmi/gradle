# gradle

yum install java-11 -y
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

so you can build 
gradle clean build

Use this link to configure gradle nexus configs
vi build.gradle
#7     id "maven-publish"
#36
publishing {
 publications {
 maven(MavenPublication) {
   //bootJar is the default build task configured by spring boot
   artifact bootJar
 }
}
repositories {
maven {
name 'nexus'
url "http://192.168.0.35:8081/repository/maven-snapshots/"
credentials {
username "admin"
password "password"
   }
  }
 }
}

save and exit
then run 
gradle publish


if we want save artifact of a build and not snapshot...then we modify the version and configure this way

publishing {
   publications {
       maven(MavenPublication) {
   //bootJar is the default build task configured by spring boot
           artifact bootJar
       }
   }

   repositories {
       maven {
name 'nexus'
if(project.version.endsWith('-SNAPSHOT')) {
url "http://192.168.0.35:8081/repository/maven-snapshots/"
} else {
url "http://192.168.0.35:8081/repository/maven-releases/"
}
credentials {
username "admin"
password "password"
   }
  }
 }
}


************
not also good to put username and password open ...rather use:

username project.repoUser
password project.repoPassword

then open a file inthe same location and put 
repoUser admin
repoPassword password

********
to download your build jar file
go to nexus - maven-snapshot
click on the jar file - copy the path

com/cloudtechmasters/springboot-maven-course-micro-svc/0.0.2-SNAPSHOT/springboot-maven-course-micro-svc-0.0.2-20230228.193356-2.jar


then also copy the maven-snapshots link  and merge it together then do wget
http://192.168.0.35:8081/repository/maven-snapshots/

wget http://192.168.0.35:8081/repository/maven-snapshots/com/cloudtechmasters/springboot-maven-course-micro-svc/0.0.2-SNAPSHOT/springboot-maven-course-micro-svc-0.0.2-20230228.193356-2.jar

wget --user admin --password password http://192.168.0.35:8081/repository/maven-snapshots/com/cloudtechmasters/springboot-maven-course-micro-svc/0.0.2-SNAPSHOT/springboot-maven-course-micro-svc-0.0.2-20230228.193356-2.jar

