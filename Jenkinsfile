pipeline {
    agent any

	environment {
        FROM="${env.FROM_EMAIL}"
		TO="${env.TO_EMAIL}"
    }
    
    stages {

		stage('Pre-Build Email') {
            steps {
                script {
                    mail subject: 'My Jenkins Pipeline Started',
                         body: "My Jenkins Pipeline has started. Click the following link to view the build status: ${env.BUILD_URL}",
                         from: "${FROM}",
                         to: "${TO}"
                }
            }
        }
		stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }


        stage('Checkout') {
    		steps {
                git branch: 'main', url: "https://github.com/meta-ankit-kumar/Jenkins-Intermediate-Goal.git",
                credentialsId: 'jenkins-git-token'
				}
    	}

        
        stage('Build') {
            steps {
                sh 'npm install'
			}
        }
        
        stage('Deploy') {
            steps {
                sh 'npm run deploy'
            }
        }
	}

	post {
        always {
            script {
                mail subject: 'My Jenkins Pipeline Run',
                    body: "My Jenkins Pipeline has finished running. Build link: ${env.BUILD_URL}",
                    from: "${FROM}",
                    to: "${TO}"
            }
        }
        success {
            script {
                mail subject: 'My Jenkins Pipeline Succeeded',
                    body: "My Jenkins Pipeline has succeeded. Build link: ${env.BUILD_URL}",
                    from: "${FROM}",
                    to: "${TO}"
            }
        }
        failure {
            script {
                mail subject: 'My Jenkins Pipeline Failed',
                    body: "My Jenkins Pipeline has failed. Build link: ${env.BUILD_URL}",
                    from: "${FROM}",
                    to: "${TO}"
            }
        }
    }
}
