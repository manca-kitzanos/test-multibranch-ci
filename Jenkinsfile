pipeline {
  agent any
  options {
    buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')
  }
  stages {
    stage('Master Branch Deploy Code') {
        when {
            branch 'main'
        }
        steps {
            sh """
            echo "Building from Main branch"
            """

            sh """
            echo "Deploying Code from Main branch"
            """
        }
    }
    stage('Develop Branch Deploy Code') {
        when {
            branch 'develop'
        }
        steps {
            sh """
            echo "Building from Develop branch"
            """
            sh """
            echo "Deploying from Develop branch"
            """
       }
    }
  }
}
