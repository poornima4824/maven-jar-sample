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
    }
}
