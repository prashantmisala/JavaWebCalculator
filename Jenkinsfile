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
            steps {
            echo 'testing'
            sh 'mvn sonar:sonar -Dsonar.host.url=http://34.201.13.80:9000 -Dsonar.login=eda5318fee51e826919ffc00c681fc9ec5869c36'
            }
        }
        stage('nexus') { 
            steps {
            echo 'uploading'
            sh 'mvn deploy'
            }
        }
        stage('tomcat'){
            steps {
            sshagent(['centos']) {
            sh 'scp -o StrictHostKeyChecking=no -r /var/lib/jenkins/workspace/prac/target/WebAppCal-0.0.1 centos@172.31.5.128:/home/centos/apache-tomcat-7.0.94/webapps/'
            }
        }
      }

    }
}
