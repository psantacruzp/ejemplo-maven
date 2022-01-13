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
		
		stage('Sonarr') {
            steps {
                script {
                    bat "mvn clean verify sonar:sonar -Dsonar.projectKey=ejemplo-maven-developer -Dsonar.host.url=http:localhost:9000 -Dsonar.login=63e507533300f7aa97b93ebb5b7dfd050cf6dacb"
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
