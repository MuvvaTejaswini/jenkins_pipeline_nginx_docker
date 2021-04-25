pipeline {
agent {label 'slave'}
  stages {
    stage('Cloning our Git') {
      agent {label 'slave'}
      steps {
        git 'https://github.com/MuvvaTejaswini/jenkins_pipeline_nginx_docker.git'
      }
    }
    stage('Docker Build') {
      agent {label 'slave'}
      steps {
        sh 'docker build -t nginx/tejaswini:assignment-1 .'
      }
    }
   stage('Docker Push') {
     agent {label 'slave'}
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhubid', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker tag nginx/tejaswini:assignment-1 mypresentdocker/assignment-1'
          sh 'docker push bala4636/assignment-1'
          sh 'docker run -it -d -p 80:80 mypresentdocker/assignment-1:latest'
        }
      }
    }

    }
  }
