pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-roza')
	}

	stages {

		stage('Build') {

			steps {
				sh 'sudo docker build -t ra1mova/awesome-cat-front awesome_cats_frontend'
			}
		}
    stage('Build2') {

      steps {
        sh 'sudo docker build -t ra1mova/awesome-cat-back awesome_cats_backend'
      }
    }
		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'sudo docker push ra1mova/awesome-cat-front'
			}
		}
    stage('Push2') {
      
      steps {
        sh 'sudo docker push ra1mova/awesome-cat-back'
      }
    }
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
