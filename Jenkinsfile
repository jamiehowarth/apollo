pipeline {
 agent {
   label 'linux'
 }
 environment {
   GIT_COMMITTER_NAME = 'jenkins'
 }
 options {
   timeout(time: 1, unit: 'HOURS')
 }
 stages {
   stage('Initialize') {
     steps {
       sh 'cp scripts/AGREEMENT.txt ${HOME}/.apollo_agreement.txt'
       sh './docker/scripts/dev_start.sh -t dev-x86_64-20180806_1111'
     }
   }
   stage('Lint') {
     steps {
       sh './apollo_docker.sh lint'
     }
   }
 }
 post {
   always {
 //   deleteDir()
   }
 }
}
