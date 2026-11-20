pipeline {

    agent any

    stages {

        stage('CHECKOUT') {
            steps {
                echo 'Descargando codigo'
                checkout scm
            }
        }

        stage('BUILD') {
            steps {
                echo 'Preparando aplicacion'
                sh 'ls -la'
            }
        }

        stage('TEST') {
            steps {
                echo 'Validando archivos'
                sh 'test -f index.html'
                sh 'test -f Dockerfile'
            }
        }

        stage('DOCKER BUILD') {
            steps {
                echo 'Construyendo imagen Docker'
                sh 'docker build -t practica-devops .'
            }
        }

        stage('DEPLOY') {
            steps {
                echo 'Desplegando aplicacion'

                sh '''
                    docker rm -f practica-devops || true

                    docker run -d \
                    --name practica-devops \
                    -p 8081:80 \
                    practica-devops
                '''
            }
        }
    }

    post {
        success {
            echo 'PIPELINE EXITOSO'
        }

        failure {
            echo 'PIPELINE FALLIDO'
        }
    }
}
