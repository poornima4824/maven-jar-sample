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
        stage('Nexus Upload') {
            steps {
             script {
                  def readPom = readMavenPom file: 'pom.xml'
                  //def nexusrepo = readPom.version.endsWith("SNAPSHOT") ? "maven-snapshots" : "maven-releases"
                  nexusArtifactUploader artifacts: 
                  [
                      [
                          artifactId: "${readPom.artifactId}",
                          classifier: '', 
                          file: "target/${readPom.artifactId}-${readPom.version}.jar", 
                          type: 'war'
                      ]
                 ], 
                         credentialsId: 'nexus', 
                          groupId: "${readPom.groupId}", 
                          nexusUrl: '3.144.132.81:8081', 
                          nexusVersion: 'nexus3', 
                          protocol: 'http', 
                          repository: "Rollback_mechanism", 
                          version: "${GIT_COMMIT}"

             }
          }
      }
    }
}
