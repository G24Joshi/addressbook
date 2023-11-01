pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "3.9.4"
    }
   stages{
      stage('Build Maven'){
          steps{
            checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/G24Joshi/addressbook.git']])
            sh 'mvn clean install'
          }
      }
            stage('Build image'){
              steps{
                  script{
                     sh 'docker build -t gjoshi24/addressbook:v1 .'
                  }
              }
          }
            stage('Push image to DockerHub'){
              steps{
                  script{
                      withCredentials([string(credentialsId: 'dockerhbpwd', variable: 'dockerhbpwd')]) {
                      sh 'docker login -u gjoshi24 -p ${dockerhbpwd}'
                           }
                      sh 'docker push gjoshi24/addressbook:v1'
                  }
              }
         }
      }
   }
