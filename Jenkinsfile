pipeline {
    agent any
    tools {
        nodejs "node"
    }
    triggers { // Configure automatic triggers
        githubPush( // Trigger on push to GitHub repository
            branches: "master", // Monitor the "master" branch
            activities: '*/**' // Trigger on any push event to the branch
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
                        to: 'mary.njuguna@student.moringaschool.com', // Replace with recipient email
                        subject: 'Gallery Tests Failed - Build $BUILD_NUMBER',
                        body: 'Tests failed for build number $BUILD_NUMBER. Check the Jenkins console for details.',
                        contentType: 'text/html' // Optional: Set content type for HTML formatting
                    )
                }
            }
        }
        stage("Start server (for demo)") { // Optional stage for demo purposes
            when { // Optional stage only runs if tests succeed
                expression { return $currentBuild.currentResult == 'SUCCESS' }
            }
            steps {
                sh 'node server' // Start the server using node server
            }
        }
    }
}