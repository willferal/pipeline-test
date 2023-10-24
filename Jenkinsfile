pipeline {
    agent{ 
        docker {
	    image 'api_flask_postgres'
        }
    }
    stages {
        stage("Checkout") {
            steps {
                    checkout([$class: 'GitSCM',
                        branches: [
                            [name: 'main']
                        ],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [[$class: 'LocalBranch', localBranch: "**"]],
                        submoduleCfg: [],
                        userRemoteConfigs: [
                            [credentialsId: 'github-account', url: 'https://github.com/willferal/pipeline-test']
                        ]
                    ])
                }
	}
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
    }
}
