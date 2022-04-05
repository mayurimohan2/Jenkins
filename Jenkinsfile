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
                    sh 'pip install --upgrade setuptools'
                }
            }
        }
        stage('complie'){
         steps {
                //This sh step runs the Python command to compile your application and
                //its calc library into byte code files, which are placed into the sources workspace directory
                sh 'python -m py_compile sources/netman_netconf_obj2.py'
                //This stash step saves the Python source code and compiled byte code files from the sources
                //workspace directory for use in later stages.
                stash(name: 'compiled-results', includes: 'sources/*.py*')
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

