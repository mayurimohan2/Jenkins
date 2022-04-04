pipeline {
    agent any
    stages {
        stage('Checkout project') {
            steps {
                script {
                    git branch: "master",
                        credentialsId: '0e07d668a4744d15afc6cb13da8623cf',
                        url: 'https://github.com/mayurimohan2/Jenkins.git'
                }
            }
        }
        stage('Installing packages') {
            steps {
                script {
                    sh 'pip install ipaddress'
                }
            }
        }
    }
}
    
