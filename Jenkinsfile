pipeline {
    agent any
    tools {
        nodejs "node"
    }
    stages {
        stage("Clone code") {
            steps {
                git branch: 'master', url: 'https://github.com/Mary-softeng/gallery.git'
                sh 'npm install'
            }
        }
        stage("Run tests") {
            steps {
                sh 'npm test' // Execute the tests using npm test
            }
            post { // Post-build actions for this stage
                success { // Only send email if the tests succeed
                    echo 'Tests passed!'
                }
                failure { // Send email notification on test failure
                    emailaction( // Configure email notification
                        to: 'mary.njuguna@student.moringaschool.com', // Replace with recipient email
                        subject: 'Gallery Tests Failed - Build $BUILD_NUMBER',
                        body: 'Tests failed for build number $BUILD_NUMBER. Check the Jenkins console for details.',
                        contentType: 'text/html' // Optional: Set content type for HTML formatting
                    )
                }
            }
        }
    }
}