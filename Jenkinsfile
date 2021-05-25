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
        stage('scanning') { 
            steps {
            sh 'mvn sonar:sonar -Dsonar.host.url=http://3.239.68.82:9000 -Dsonar.login=787c840b01beb225671ea3580e894f69e1e71422'
            }
        }
        stage('nexxus'){
            stage {
	    sh 'mvn deploy'
            }
        }
    }
}
