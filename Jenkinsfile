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
                    sh 'pip install prettytable'
                    sh 'pip install ncclient'
                    sh 'pip install pandas'
                    sh 'pip install netaddr'
                }
            }
        }
    }
}
 post {
        always {
            echo 'I will always say Hello again!'
            
            emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
            
        }
    }
}    
