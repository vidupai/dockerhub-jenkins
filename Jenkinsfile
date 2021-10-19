pipeline {
	agent any
	environment {
	DOCKERHUB_CREDENTIALS = credentials('vidupai-dockerhub')
	}
    stages {
	stage('Example') {
            steps {
                echo 'Hello World!!'
            }
        }
	    
	stage('Start') {
            steps {
                sh 'ls -lrt'
		sh 'date'
		sh 'pwd'
		sh 'docker -version'
		sh 'java -version'
            }
        }


        stage('Build') {
            steps {
                sh 'docker build -t vidupai/vidupai2012:latestlocal .'
            }
        }
		
	stage('Login') {
		steps {
		  sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
		}
	}
		
        stage('Push') {
            steps {
                sh 'docker push vidupai/vidupai2012:latestlocal'
            }
        }
    }
	post {
		always {
			sh 'docker logout'
		}
	}
}
