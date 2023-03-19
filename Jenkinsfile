pipeline {
    agent any
    
    stages {
        stage('Checkout') {
    		steps {
    		    withCredentials([usernamePassword(credentialsId: 'f6849c6e-5c5b-4e0f-8239-7e7955dc4a90', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
    		        git branch: 'main', url: 'https://USERNAME:PASSWORD@github.com/meta-ankit-kumar/Jenkins-Intermediate-Goal.git'
    		    }
    		}
		}

        
        stage('Build') {
            agent {
                docker { 
                    image 'my-docker-image' 
                    args '-u root'
                }
            }
            
            steps {
                sh 'npm install'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'npm run deploy'
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
}
