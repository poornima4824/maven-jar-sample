pipeline {
agent any
tools {
    maven 'maven'
}   
    stages {
        stage('Code checkout') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/poornima4824/maven-jar-sample.git']]])
                
                } 
            }
        }
        stage('Build') { 
            steps {
                sh "mvn clean package"
            }
        }
        stage('Upload Artifacts To Nexus') {
            steps {
                script {
                    nexusArtifactUploader artifacts:
                    [
                        [
                            artifactId: 'build_artifact',
                            classifier: '',
                            file: "target/maven-jar-sample-1.0.jar",
                            type: 'war'
                        ]
                    ],
                    credentialsId: 'nexus',
                    groupId: 'build',
                    nexusUrl: '3.144.132.81:8081',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: 'Rollback_mechanism',
                    version: "${GIT_COMMIT}"
                }
            }
        }
    }
}
