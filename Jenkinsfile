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
                    sh 'pip install pandas'
                    sh 'pip install netaddr'
                    sh 'python -m pip install pylint'
                }
            }
        }
        stage('Linting') { // Run pylint against your code
      steps {
        script {
          sh """
          pylint netman_netconf_obj2.py
          """
        }
      }
    }
    }
     post {
        always {
            echo 'I will always say Hello again!'
            
             emailext attachLog: true, body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:

Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'mamo5332@colorado.edu'
            
        }
    }
}

