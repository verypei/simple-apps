pipeline {
    agent {label 'devops-1-very'}
    tools{nodejs 'nodejs-18.16.0'}
    stages {
        stage('Checkout GIT') {
            steps {
                git branch: 'main', url: 'https://github.com/verypei/simple-apps.git'
            }
        }

        stage('run NPM INSTALL') {
            steps {
                sh '''npm install
                '''
            }
        }
    
        stage('run SONAR QUBE') {
            steps {
                sh '''sonar-scanner  \ 
                -Dsonar.projectKey=simple-apps  \
                 -Dsonar.sources=.  \
                  -Dsonar.host.url=http://172.23.1.21:9000  \
                   -Dsonar.login=sqp_59c547e97eb76f988e19e5029e1aee103e9048cf'
                   '''
            }
        }
    
        stage('DOCKER COMPOSE') {
            steps {
                sh '''docker compose build
                docker compose build -d
                '''
            }
        }
    }
}