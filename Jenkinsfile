pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh '''
                      pip install -r requirements.txt 
                   '''
            }
        }
        stage('Scan') {
            steps {
                echo 'Scanning..'
                sh '''
                      FASTAPI_ENV=test python3 -m uvicorn src.main:app &
                      curl -Lo mapi https://mayhem4api.forallsecure.com/downloads/cli/latest/linux-musl/mapi && chmod +x mapi
                   '''
                withCredentials([string(credentialsId: 'MAPI-TOKEN', variable: 'MAPI-TOKEN')]) {
                    sh './mapi login ${MAPI_TOKEN}'
                }
                sh '''
                      ./mapi run forallsecure-mapi-action-examples auto "http://localhost:8000/openapi.json" --url "http://localhost:8000/" --junit junit.xml --sarif mapi.sarif --html mapi.html
                   '''
            }
        }
        stage('Archive') {
            steps {
                echo 'Archive....'
            }
        }
    }
}
