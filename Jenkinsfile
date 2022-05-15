pipeline {
  agent any
  stages {
    stage('Quality Gate') {
      steps {
          echo 'Quality Gate'     
      }
    }
    stage('Unit Testing') {
      when {
            // anyOf {branch 'ft_*'; branch 'bg_*'}
            branch 'do_not_run'
        }
        steps {
            withMaven {
                sh 'cd recipe-api'
                sh 'mvn test'
                sh 'cd ../email-api'
                sh 'mvn test'
            }
            junit skipPublishingChecks: true, testResults: 'target/surefire-reports/*.xml'
        }
    }
    stage('Build') {
      when {
          branch 'main'
      }
      steps{
          withMaven {
              sh 'cd recipe-api'
              sh 'mvn package -DskipTests'
          }
      }

    }
    stage('Docker Image') {
      steps {
          echo 'Docker Image'
      }
    }
    stage('Docker Deliver') {
      steps {
          echo 'Docker Deliver'     
      }
    }
    stage('Wait for approval') {
      steps {     
          echo 'Wait for approval'
      }
    }
    stage('Deploy') {
      steps {
          echo 'Deploy'
      }
    }
  }
}