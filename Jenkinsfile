pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh '''
                      pip install -r requirements.txt 
                      FASTAPI_ENV=test uvicorn src.main:app &
                   '''
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
              
            }
        }
        stage('Archive') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
