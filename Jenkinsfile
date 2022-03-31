pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh './mvnw package'
      }
    }

    stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv('sonar') {
          sh './mvnw clean verify sonar:sonar -Dsonar.projectKey=sonar'
        }

        waitForQualityGate true
      }
    }

    stage('artifact') {
      steps {
        archiveArtifacts 'target/*.jar'
      }
    }

  }
}