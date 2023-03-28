pipeline{

    agent any

    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub-roza')
    }

    stages {

        stage('Build') {

            steps {
                sh 'sudo docker build -t ra1mova/awesome-cat-frontend awesome_cats_frontend'
            }
        }
        stage('Build2') {

            steps {
                sh 'sudo docker build -t ra1mova/awesome-cat-backend awesome_cats_backend'
            }
        }
        stage('Login') {

            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push') {

            steps {
                sh 'sudo docker push ra1mova/awesome-cat-frontend'
            }
        }
        stage('Push2') {

            steps {
                sh 'sudo docker push ra1mova/awesome-cat-backend'
            }
        }
    }

    post {
        always {
                sh 'docker logout'
        }
    }
}

