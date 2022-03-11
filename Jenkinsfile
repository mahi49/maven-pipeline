pipeline {
    agent any
	tools {
              jdk "JAVA_HOME"
	      maven "MAVEN_HOME"
        }

    stages {
        stage('Checkout-git') {
            steps {
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'mahender', url: 'https://github.com/mahi49/maven-pipeline.git']]])      }
        }
    
     stage('Validate') {
            steps {
                sh 'mvn validate'
        }
    }
    
     stage('compile_code') {
            steps {
                sh 'mvn compile'
        }
    }
      stage('Test') {
            steps {
                sh 'mvn test'
        }
    }
     stage('Package') {
            steps {
                sh 'mvn package'
        }
    }
	     stage('deploy') {
            steps {
               sshagent(['tomcat-USER']) {
               sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pipeline-project2/target/maven-web-application.war ubuntu@3.91.62.183:/opt/apache-tomcat-9.0.59/webapps"
        }
        }
    }
	}
}
