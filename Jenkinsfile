pipeline {
  agent any
  environment {
    registryCredential = 'dockerhub'
  }
  stages {
    stage('TestBuild') {
      steps {
        sh 'docker build -t mohsinejaz/project-fib-test-client -f Dockerfile.dev .'
     } 
   }
   stage('Test') {
      steps {
        sh 'docker container rm -f client || true'
        sh 'docker container run --name client -d mohsinejaz/project-fib-test-client npm test -- --coverage'
      } 
   }
   stage('build') {
	steps {
	  sh 'docker build -t mohsinejaz/project-fib-client .'
           }
      }
    stage('Publish') {
        steps{
            script {
                docker.withRegistry( '', registryCredential ) {
		 sh 'docker push mohsinejaz/project-fib-client:latest'
               } 
           }
        }       
    }
  }
}
