pipeline {
    agent any

    stages {
        stage('Clone sources') {
            steps {
                sh git clone 'https://github.com/aklot07/java-maven-app.git'
            }
        }

        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh "./gradlew sonarqube"
                }
            }
        }
        stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
    }
}
