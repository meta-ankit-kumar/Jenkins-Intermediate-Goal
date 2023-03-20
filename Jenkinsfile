pipeline {
    agent any
    
    stages {

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
				dir('Jenkins-Intermediate-Goal') {
                    sh 'npm install'
                }
			}
        }
        
        stage('Deploy') {
            steps {
                dir('Jenkins-Intermediate-Goal') {
                    sh 'npm deploy'
                }
            }
        }
	}

		post {
        always {
            script {
                mail subject: 'My Jenkins Pipeline Run',
                     body: 'My Jenkins Pipeline has finished running.',
                     from: 'dev.ankit029@gmail.com',
                     to: 'ankit.kumar@metacube.com'
            }
        }
        success {
            script {
                mail subject: 'My Jenkins Pipeline Succeeded',
                     body: 'My Jenkins Pipeline has succeeded.',
                     from: 'dev.ankit029@gmail.com',
                     to: 'ankit.kumar@metacube.com'
            }
        }
        failure {
            script {
                mail subject: 'My Jenkins Pipeline Failed',
                     body: 'My Jenkins Pipeline has failed.',
                     from: 'dev.ankit029@gmail.com',
                     to: 'ankit.kumar@metacube.com'
            }
        }
    }
}
