pipeline {
agent {
    label 'linux'
   // docker {
   //     image 'docker:dind'
   // }
} 
//agent any
 
 environment {
   GIT_COMMITTER_NAME = 'jenkins'
 }
 options {
   timeout(time: 2, unit: 'HOURS')
 }
 stages {
   stage('Initialize') {
     steps {
       sh 'cp scripts/AGREEMENT.txt ${HOME}/.apollo_agreement.txt'
       sh './docker/scripts/dev_start.sh -t dev-x86_64-20180806_1111'
     }
   }
   stage('lint') {
     steps {
       sh './apollo.sh lint'
     }
   }
  stage('cibuild') {
     steps {
       sh './apollo_docker.sh cibuild'
     }
   }
  stage('citest_basic') {
     steps {
       sh './apollo_docker.sh citest_basic'
     }
   }
  stage('citest_map') {
     steps {
       sh './apollo_docker.sh citest_map'
     }
   }
  stage('citest_dreamview') {
     steps {
       sh './apollo_docker.sh citest_dreamview'
     }
   }
  stage('citest_perception') {
     steps {
       sh './apollo_docker.sh citest_perception'
     }
   }
 }
 post {
   always {
    deleteDir()
   }
 }
}
