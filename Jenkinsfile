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
		    sh 'scripts/deliver.sh'
			}
                   }
               }
           }
	    stage ('Run JFrog CLI') {

            steps {
		sh 'touch ak'
		archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
                rtUpload (
    				serverId: 'AK-Artifactory',
    				spec: '''{
          			"files": [
           			 {
             			 "pattern": "target/*.jar",
             			 "target": "example-repo-local/"
            			}
         			]
    			}'''

            	)

        }
        }
    }
}
