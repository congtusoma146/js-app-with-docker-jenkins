pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {

		stage('gitclone') {

			steps {
				git 'https://github.com/nguyenbuitk/js-app-with-docker-jenkins.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t buinguyen/js-app-docker-container:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push buinguyen/js-app-docker-container:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
