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
                  def nexusrepo = readPom.version.endsWith("SNAPSHOT") ? "maven-snapshots" : "maven-releases"
                  nexusArtifactUploader artifacts: 
                  [
                      [
                          artifactId: "${readPom.artifactId}",
                          classifier: '', 
                          file: "target/build_artifact-1.0.jar", 
                          type: 'jar'
                      ]
                 ], 
                         credentialsId: 'nexus', 
                          groupId: "${readPom.groupId}", 
                          nexusUrl: '3.144.132.81:8081', 
                          nexusVersion: 'nexus3', 
                          protocol: 'http', 
                          repository: "${nexusrepo}", 
                          version: "${GIT_COMMIT}"

             }
          }
      }
    }
}
