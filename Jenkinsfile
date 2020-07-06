pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'build demo-app'
        bat 'run_build_script.bat'
      }
    }

    stage('Linux Tests') {
      parallel {
        stage('Linux Tests') {
          steps {
            echo 'Run linux tests'
          }
        }

        stage('Windows Tests') {
          steps {
            echo 'Run windows tests'
          }
        }

      }
    }

    stage('Deploy Staging') {
      steps {
        echo 'Deploy to staging env'
        input 'Ok to deploy to prod?'
      }
    }

    stage('Deploy prod') {
      steps {
        echo 'Deploy to prod'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'ci-team@example.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}