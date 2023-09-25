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
      environment {
        github_branch = "master"
        dockerimagename = "devteambflows/bflows-api-production"
        dockerImage = ""
        registryCredential = 'dockerhublogin'
      }
      steps {
        git branch: "${github_branch}", url: 'https://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@github.com/rbonazzo-KZ/Bflows-core.git'
        script {
          sh 'mvn clean install -Dmaven.test.skip=true -Dspring.profiles.active=production'
        }
        script {
          dockerImage = docker.build dockerimagename
        }
        script {
          docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
            dockerImage.push("latest")
          }
        }
      }
    }
  }
}
