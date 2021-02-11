pipeline {
    agent any
    tools { 
        maven 'Maven_Home' 
       // jdk 'jdk8' 
    }
    stages {
        stage("Clone code from VCS") {
            steps {
                script {
            steps {

                   git branch: 'jenkins_pipeline_success', changelog: false, poll: false, url: 'https://github.com/PRASAD4CNET/VProfile.git/';
                }
            }
        }
        stage("Maven Build") {
            steps {
                script {
                    sh 'mvn clean package'
                    //sh "mvn package -DskipTests=true"
                }
            }
        }
        stage("Sonar Analysis") {
            steps {
                script {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=avulam -Dsonar.host.url=http://10.5.5.6:9000 -Dsonar.login=a33845bcb6113d651c8f80bbffdad5a7d1fd9b20'
                    
                }
            }
        }
        stage("Publish to Nexus Repository Manager ") {
            steps {
                script {
                        nexusArtifactUploader artifacts: [[artifactId: 'vprofile', classifier: '', file: 'target/vprofile-2.0.0.war', type: 'war']], credentialsId: '9056eeb9-1b6c-4652-bf56-e8f6248d09fa', groupId: 'com.carleton', nexusUrl: '10.5.5.7:8090', nexusVersion: 'nexus3', protocol: 'http', repository: 'testdemo-release', version: '1.0.0'
                }
            }
        }
        stage("Publish to Nexus Repository Manager empty") {
            steps {
                script {
                    sh 'echo avulam'
                    
                }
            }
        }
    }
}
}
