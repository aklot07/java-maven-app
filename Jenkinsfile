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
		sh 'touch ak'
                rtUpload (
    				serverId: 'AK-Artifactory',
    				spec: '''{
          			"files": [
           			 {
             			 "pattern": "ak",
             			 "target": "example-repo-local/"
            			}
         			]
    			}'''

            	)

        }
        }
    }

