pipeline {
	agent{
		label 'Built-In Node'
	}
	environment {
	DOCKERHUB_CREDENTIALS = credentials('vidupai-dockerhub')
	}
    stages {
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
