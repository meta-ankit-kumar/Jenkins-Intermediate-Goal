pipeline {
    agent any
    
    stages {
        stage('Checkout') {
    		steps {
    		    withCredentials([usernamePassword(credentialsId: 'f6849c6e-5c5b-4e0f-8239-7e7955dc4a90', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
    		        git branch: 'main', url: 'https://USERNAME:PASSWORD@github.com/https://github.com/meta-ankit-kumar/Jenkins-Intermediate-Goal.git'
    		    }
    		}
		}

		stage('Send Pre-Build Email Notification') {
            steps {
                sh 'echo "Your build is starting now" | mail -s "Build Started" ankit.kumar@metacube.com'
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

		stage('Send Post-Build Email Notification') {
            steps {
                sh 'echo "Your build has finished" | mail -s "Build Finished" ankit.kumar@.com'
            }
        }
    }
}
