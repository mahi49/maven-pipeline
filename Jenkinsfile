pipeline {
    agent any
	tools {
              jdk "JAVA_HOME"
	      maven "MAVEN_HOME"
        }

    stages {
        stage('Checkout') {
            steps {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'devopsdeepdive', url: 'https://github.com/devopsdeepdive/maven-pipeline.git']]])            }
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
               sshagent(['tomcat-user']) {
               sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/demo-pipeline-project/target/maven-web-application.war ubuntu@54.175.211.150:/opt/apache-tomcat-9.0.59/webapps"
        }
        }
    }
	}
}
