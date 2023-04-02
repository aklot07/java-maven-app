pipeline {
    agent any
	environment {

        JFROG_CLI_BUILD_NAME = "${env.JOB_NAME}"

        JFROG_CLI_BUILD_NUMBER = "${env.BUILD_NUMBER}"

    }
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

        /*stage('SonarQube analysis') {
            steps {
		   dir ('java-maven-app'){ 
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn clean package sonar:sonar'
		    archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
		    sh 'scripts/deliver.sh'
			}
                   }
               }
           }*/
	    stage ('Run JFrog CLI') {

            steps {

                sh 'jfrog rt mvn -f /java-maven-app clean install' // build & deploy artifacts

                sh 'jfrog rt bp' // publish build info

            }

        }
        }
    }

