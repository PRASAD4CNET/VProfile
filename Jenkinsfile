pipeline {

    agent any
tools { 
        maven 'Maven_Home' 
       // jdk 'jdk8' 
    }

    environment {
    //Use Pipeline Utility Steps plugin to read information from pom.xml into env variables
    IMAGE = readMavenPom().getArtifactId()
    VERSION = readMavenPom().getVersion()
    }


    stages {

        stage('Test') {
            steps {
                echo "${VERSION}"
            }

        }

    }

}

