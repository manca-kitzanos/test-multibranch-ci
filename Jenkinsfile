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
        git branch: "${github_branch}", url: 'https://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@github.com/Kitzanos/bflows-api.git'
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
