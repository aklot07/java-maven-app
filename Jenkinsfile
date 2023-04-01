pipeline {
    agent any

    stages {
        stage ('clean up') {
	        steps {
	            cleanWs()
	        }
	    }
        stage('Clone sources') {
            steps {
                sh 'git clone https://github.com/aklot07/java-maven-app.git'
            }
        }

        stage('SonarQube analysis') {
            steps {
		   dir ('java-maven-app'){ 
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn clean package sonar:sonar'
			}
                }
            }
        }
        stage("Quality gate") {
            steps {
                timeout(time: 3, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
		}
            }
        }
    }
}
