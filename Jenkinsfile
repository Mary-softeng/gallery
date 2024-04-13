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
                sh 'npm test' // Execute the tests using npm test
            }
            post { // Post-build actions for this stage
                success {
                    echo 'Tests passed!'
                }
                failure {
                    emailaction( // Configure email notification
                        to: 'mary.njuguna1@student.moringaschool.com', // Replace with recipient email
                        subject: 'Gallery Tests Failed - Build $BUILD_NUMBER',
                        body: 'Tests failed for build number $BUILD_NUMBER. Check the Jenkins console for details.',
                        contentType: 'text/html' // Optional: Set content type for HTML formatting
                    )
                }
            }
        }
      
    }
    post {
        always{
            slackSend channel: 'devops-project', message: 'Week2_Ip'
        }
    }
}