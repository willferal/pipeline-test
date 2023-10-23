pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh'''
		    docker stop api-flask
		    docker rmi api_flask_postgres:1.0.0
		    docker build -t api_flask_postgres:1.0.0 .
		    docker compose up -d api-flask
		'''
            }
        }
        stage('Test') {
            steps {
                curl http://localhost:4000/test
            }
        }
        stage('Deploy') {
            steps {
                //
            }
        }
    }
}
