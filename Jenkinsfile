pipeline{
    agent any
    tools{
        nodejs "node"
    }
    stages{
        stage("clone code"){
            steps{
                git branch:'master', url:'https://github.com/Mary-softeng/gallery.git'
                sh 'npm install'
            }
            
        }
   
    }
}