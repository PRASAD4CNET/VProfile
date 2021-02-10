pipeline {
    agent any
    stages {
        stage("Clone code from VCS") {
            steps {
                script {
                   git branch: 'jenkins-test', changelog: false, poll: false, url: 'https://github.com/PRASAD4CNET/VProfile.git/';
                }
            }
        }
        stage("Maven Build") {
            steps {
                script {
                    sh 'mvn clean install'
                    //sh "mvn package -DskipTests=true"
                }
            }
        }
        stage("Sonar Analysis") {
            steps {
                script {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=avulam -Dsonar.host.url=http://10.5.5.6:9000 -Dsonar.login=b3dcee08d2d4702732fe535ca314268cf5f875e2'
                    }
                }
            }
        }
        stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                    nexusArtifactUploader credentialsId: '9056eeb9-1b6c-4652-bf56-e8f6248d09fa', groupId: 'com.carleton', nexusUrl: '10.5.5.7:8090', nexusVersion: 'nexus3', protocol: 'http', repository: 'deployment', version: '4.0.5'
                    }
                }
            }
        }
        stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                    }
                }
            }
        }
    }
}
