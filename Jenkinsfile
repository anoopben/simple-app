pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'jdk 8'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                script{
                      nexusArtifactUploader artifacts: [
                            [artifactId: 'simple-app',
                             classifier: '',
                             file: 'target/simple-app-3.0.0-SNAPSHOT.war',
                             type: 'war'
                              ]
                            ],
                      credentialsId: 'nexus-cred',
                      groupId: 'in.javahome',
                      nexusUrl: '192.168.1.164:8081',
                      nexusVersion: 'nexus3',
                      protocol: 'http',
                      repository: 'http://192.168.1.164:8081/repository/repository-example/',
                      version: '3.0.0-SNAPSHOT'
                    }
            }
        }
}

