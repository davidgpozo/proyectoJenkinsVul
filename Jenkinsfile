pipeline {
    agent any
    stages {
        stage('Docker Build') {
            steps {
                sh 'docker build -t jenkinstest:latest .'
            }
        }
        stage('TEST') {
            steps {
                echo 'test'
                sh 'docker run --name jenkinstest -id -p 80:80 jenkinstest:latest'
                sh '/bin/nc -vz localhost 80'
            }
	    post {
		always{
			sh 'docker container stop jenkinstest'
			sh 'docker rm jenkinstest'
                }
            }
        }
        stage('Push Registry Docker Hub') {
            steps {
                echo 'deploy'
		sh 'docker tag jenkinstest:latest shefirot/jenkinstest:stable'
		sh 'echo duffel_test_Hwmb7ksyyRx0pi6Fgh1uiEcRTUrosEDumi78ZkAY98Z'
		sh 'echo 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'
		sh 'echo BjBNrzx7HYsxegAtqd1e'
		sh 'echo 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m'
		withDockerRegistry(credentialsId: 'dockerHubShefi', url: 'https://index.docker.io/v1/') {
			sh 'docker push shefirot/jenkinstest:stable'
		}
            }
        }
    }
    post {
	always {
		echo 'Hemos llegado al final'
        }
        failure {
		echo 'Pero a cascado'
        }
    }
}
