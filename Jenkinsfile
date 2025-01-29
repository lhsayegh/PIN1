pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
  }
   stages {
   stage('Building image') {
      steps{
          sh '''
          docker build -t testapp .
             '''  
        }
    }
  
  
    stage('Run tests') {
      steps {
        sh "docker run testapp npm test"
      }
    }

    stage('Run tests') {
      steps {
        sh "docker run testapp npm test"
      }
    }

  stage('Run Registry') {
      steps {
        sh "docker run -d -p 5000:5000 --name registry registry:2.7"
      }
    }
   stage('Deploy Image') {
      steps{
        sh '''
        docker tag testapp 127.0.0.1:5000/mguazzardo/testapp
        docker push 127.0.0.1:5000/mguazzardo/testapp   
        '''
        }
      }
  stage('Scan Image') {
      steps{
        sh '''
        sh "docker run aquasec/trivy image --severity=critical 127.0.0.1:5000/mguazzardo/testapp"
        '''
        }
      }
   stage('Stop Image') {
      steps{
        sh '''
        sh "docker stop   registry"
        '''
        }
      }
    }
}


    
  

