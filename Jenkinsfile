pipeline {
    agent any 
    stages {
        stage('compile') { 
            steps {
            echo 'compile'
            sh 'mvn compile'
            }
        }
        stage('package') { 
            steps {
            echo 'package'
            sh 'mvn package'
            }
        }
        agent {slave}     
        stage('sonar') { 
            steps {
            echo 'testing'
            sh 'mvn sonar:sonar -Dsonar.host.url=http://3.218.152.201:9000 -Dsonar.login=9ee09de73ce5d9404b216d986bfcdc9ee9d3db54'
            }
        }
        agent {slave}   
        stage('nexus') { 
            steps {
            echo 'uploading'
            sh 'mvn deploy'
            }
        }
    }
 }
