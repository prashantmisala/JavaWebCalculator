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
          
         stage('sonar') { 
         agent {
              label 'slave'
         }
            steps {
            echo 'testing'
            sh 'mvn sonar:sonar -Dsonar.host.url=http://34.205.92.77:9000 -Dsonar.login=8d46d1a5745eefef0508522b243aa55552a044a4'
            }
        }
           
        stage('nexus') { 
        agent { 
                 label 'slave'
            }
            steps {
            echo 'uploading'
            sh 'mvn deploy'
            }
        }
        stage('tomcat'){
            steps {
            sshagent(['centos']) {
            sh 'scp -o StrictHostKeyChecking=no -r /var/lib/jenkins/workspace/complete/target/WebAppCal-0.0.1 centos@34.205.92.77:/home/centos/apache-tomcat-7.0.94/webapps/'
            }
        }
    }
 }
}
