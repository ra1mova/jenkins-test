pipeline{

    agent any

    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }

    stages {

        stage('Build') {

            steps {
                sh 'docker build -t ra1mova/awesome-cat-frontend awesome_cats_frontend'
            }
        }
        stage('Build2') {

            steps {
                sh 'docker build -t ra1mova/awesome-cat-backend awesome_cats_backend'
            }
        }
        stage('Login') {

            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push') {

            steps {
                sh 'docker push ra1mova/awesome-cat-frontend'
            }
        }
        stage('Push2') {

            steps {
                sh 'docker push ra1mova/awesome-cat-backend'
            }
        }
    }

    post {
        always {
                sh 'docker logout'
        }
      failure {
        emailext to: "roza.raimova11@gmail.com",
        subject: "jenkins build:${currentBuild.currentResult}: ${env.JOB_NAME}",
        body: "${currentBuild.currentResult}: Job ${env.JOB_NAME}\nMore Info can be found here: ${env.BUILD_URL}"
    }
    }
}

