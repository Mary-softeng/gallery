pipeline {
    agent any
    tools {
        nodejs "node"
    }
    triggers { // Configure automatic triggers
        githubPush( 
        )
    }
    stages {
        stage("Clone code") {
            steps {
                git branch: 'master', url: 'https://github.com/Mary-softeng/gallery.git'
                sh 'npm install' // Install dependencies
            }
        }
        stage("Run tests") {
            steps {
                sh 'npm test' 
            }
            post { 
                success {
                    echo 'Tests passed!'
                }
                failure {
                    emailaction( 
                        to: 'mary.njuguna1@student.moringaschool.com', 
                        subject: 'Gallery Tests Failed - Build $BUILD_NUMBER',
                        body: 'Tests failed for build number $BUILD_NUMBER. Check the Jenkins console for details.',
                        contentType: 'text/html' 
                    )
                }
            }
        }
      
    }
    post {
        always{
            slackSend channel: 'devops-project', message: 'https://mary-njuguna-ip-deploy-34ab725b7ca9.herokuapp.com/'
        }
    }
}