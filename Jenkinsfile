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
            sh 'mvn sonar:sonar -Dsonar.host.url=http://34.231.242.10:9000 -Dsonar.login=d9716ed2d72b2f7281638a3b20cf5d1c859e2f1a'
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
            sh 'scp -o StrictHostKeyChecking=no -r /var/lib/jenkins/workspace/complete/target/WebAppCal-0.0.1 centos@34.205.92.77:/home/centos/apache-tomcat-7.0.94/webapps/'
            }
        }
    }
 }
}
