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
        stage('tomcat'){
            steps {
            sshagent(['centos']) {
            sh 'scp -o StrictHostKeyChecking=no -r /var/lib/jenkins/workspace/prac/target/WebAppCal-0.0.1 centos@172.31.20.172:/home/centos/apache-tomcat-7.0.94/webapps/'
            }
        }
      }

    }
}
