pipeline {

  agent {
    kubernetes {
      yamlFile 'builder.yaml'
    }
  }

  stages {

    stage('Deploy App to Kubernetes') {
      steps {
        container('kubectl') {
          withCredentials([file(credentialsId: 'mykubeconfig', variable: 'KUBECONFIG')]) {
            sh 'kubectl create ns brbd'
            sh 'kubectl apply -f ./manifests -n brbd'
          }
        }
      }
    }
    stage("mysql test") {
      steps {
         script {
           echo "Start of the MySQL test"
           sh "telnet 127.0.0.1 3306"
        }
      }
    }
  }
}
