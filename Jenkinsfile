pipeline {
    agent any
    tools { 
        maven 'Maven_Home' 
       // jdk 'jdk8' 
    }
    stages {
        
        stage("Maven Build") {
            steps {
                script {
                    sh 'mvn clean package'
                     def version = sh script: 'mvn help:evaluate -Dexpression=project.version -q -DforceStdout', returnStdout: true
                    
                    //sh "mvn package -DskipTests=true"
                    // Archive the built artifacts
            //archive includes: 'target/**.war'

                }
            }
        }
        stage("Maven build number") {
           steps {
               
                sh "mvn -N help:effective-pom -Doutput=pom.xml"

                    script {
                             pom = readMavenPom(file: 'pom.xml')
                                projectArtifactId = pom.getArtifactId()
                                projectGroupId = pom.getGroupId()
                                 projectVersion = pom.getVersion()
                                   projectName = pom.getName()
                                }

                         echo "Building ${projectArtifactId}:${projectVersion}"
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
                    nexusArtifactUploader artifacts: [[artifactId: 'vprofile', classifier: '', file: 'target/vprofile-$MAVEN_VERSION.war', type: 'war']], credentialsId: '9056eeb9-1b6c-4652-bf56-e8f6248d09fa', groupId: 'com.carleton', nexusUrl: '10.5.5.7:8090', nexusVersion: 'nexus3', protocol: 'http', repository: 'testdemo-release', version: '$MAVEN_VERSION'    
                    //nexusArtifactUploader artifacts: [[artifactId: 'vprofile', classifier: '', file: 'target/vprofile-2.0.0.war', type: 'war']], credentialsId: '9056eeb9-1b6c-4652-bf56-e8f6248d09fa', groupId: 'com.carleton', nexusUrl: '10.5.5.7:8090', nexusVersion: 'nexus3', protocol: 'http', repository: 'testdemo-release', version: '1.0.0'
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

