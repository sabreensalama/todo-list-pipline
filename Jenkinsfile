pipeline {
  agent any
  stages {
  stage('cloninig todo repo and building ') {
      steps {
        script {
          dir('/usr/src/app'){
                 git url: 'https://github.com/dobromir-hristov/todo-app.git'
                 sh 'cp ../Dockerfile . '
                 sh 'docker build -t todo-list-app . '
          }

        }
      }
    }
    stage('Run') { 
            steps {
                sh 'docker run --rm --name todo-e2e-tests todo-list-app yarn lint'
            }
        }
              stage('unit Test') { 
            steps {
                sh 'sudo docker run --rm --name todo-list-unit-tests todo-list-app yarn test:unit '
            }
        }

            stage('e2c Test') { 
            steps {
                sh 'sudo docker run --rm --name todo-list-e2e-tests todo-list-app yarn test:e2e --headless'
 '
            }
        }
    }
}