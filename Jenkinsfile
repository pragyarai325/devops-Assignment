pipeline {
    agent any
    environment {
		DOCKERHUB_CREDENTIALS=credentials('adarsh-devops')
	}
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AdarshN7/WebAPI_demo_DevOps.git'
            }
        }
        stage('Build') {
              steps {
                    bat 'docker build -t adarshn7/demowebapi .'
                
              }
        }
        stage('Run') {
            steps {
                bat 'docker run -d -it --rm -p 9001:5000 --name demo.container adarshn7/demowebapi:latest'
            }
        }
        stage('Docke-Hub Login') {
			steps {
			   bat 'docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PWD'
			}
		}
        
         stage('Deploy') {
            steps {
                bat 'docker push adarshn7/demowebapi:latest'
            }
        }
    }
    post {
		always {
			bat 'docker logout'
		}
	}

}
