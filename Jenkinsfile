pipeline {
 agent {
   docker {
     label ‘linux’
     image ‘dev-x86_64-20180806_1111’
     args ‘-v /tmp:/tmp -p 80:80’
   }
 }
 environment {
   GIT_COMMITTER_NAME = ‘jenkins’
 }
 options {
   timeout(30, MINUTESS)
 }
 stages {
   stage(‘Initialize’) {
     steps {
       sh ‘cp scripts/AGREEMENT.txt ${HOME}/.apollo_agreement.txt’
       sh './docker/scripts/dev_start.sh -t dev-x86_64-20180806_1111'
     }
   }
   stage(‘Lint’) {
     steps {
       sh ./apollo_docker.sh lint
     }
   }
 }
 post {
   always {
   deleteDir()
 }
 }
}
