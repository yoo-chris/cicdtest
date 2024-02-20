pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/yoo-chris/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        docker build -t chris4929/cicdtest:green .
        docker push chris4929/cicdtest:green
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        kubectl create deploy myweb2 --image=chris4929/cicdtest:green
        kubectl expose deploy myweb2 --type=LoadBalancer --port=80 --target-port=80 --protocol=TCP
        '''
      }
    }
  }
}
