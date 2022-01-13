pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                script {
                    bat "mvn clean compile -e"
                }
            }
        }
		
		stage('Sonar') {
            steps {
                script {
                    def scannerHome = tool 'sonar-scanner';
                    withSonarQubeEnv('sonar-server') {
                        bat "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-maven-developer -Dsonar.sources=src -Dsonar.java.binaries=build"
		            }
                }
			}
		}
          
        stage('Test') {
            steps {
                script {
                    bat "mvn clean test -e"
                }
            }
        }
	
        stage('Package') {
            steps {
                script {
                    bat "mvn clean package -e"
                }
            }
        }
        stage('Run') {
            steps {
                script {
                    bat "start /min mvn spring-boot:run &"
                }
            }
        }
        stage('Test Applications') {
            steps {
                script {
                    bat "start chrome http://localhost:8081/rest/mscovid/test?msg=testing"
					
                }
            }
        }
    }
}
