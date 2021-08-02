pipeline {
  agent {
    node {
      label 'centos7-slave'
    }

  }
  stages {
    stage('CheckOut Code') {
      steps {
        git(url: 'https://github.com/Foondel/NodeJS-EmptySiteTemplate.git', branch: 'master', changelog: true, poll: true)
      }
    }

    stage('Install Dependencies {Build}') {
      steps {
        sh 'npm install'
      }
    }

    stage('running the app') {
      steps {
        sh 'npm start &'
      }
    }

    stage('Test the app') {
      steps {
        sh 'sleep 5 && curl localhost:8080'
      }
    }

    stage('kill the app') {
      steps {
        sh 'sudo pkill -f node'
      }
    }

    stage('Package') {
      steps {
        sh 'zip -r package.zip .'
        archiveArtifacts 'package.zip'
        cleanWs(cleanWhenSuccess: true)
      }
    }

    stage('slack') {
      steps {
        slackSend(channel: 'a')
      }
    }

  }
}