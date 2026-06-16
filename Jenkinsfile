pipeline {
  agent any
  options { timestamps() }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests=false'
      }
    }

    stage('Unit Test') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Static Check') {
      steps {
        sh 'echo SonarQube or static scan goes here'
      }
    }

    stage('Docker Build') {
      when {
        anyOf {
          branch 'develop'
          branch 'master'
          expression { env.BRANCH_NAME?.startsWith("feature/") }
          expression { env.BRANCH_NAME?.startsWith("release/") }
          expression { env.BRANCH_NAME?.startsWith("hotfix/") }
        }
      }
      steps {
        sh 'echo Docker build and push goes here'
      }
    }
  }
}
