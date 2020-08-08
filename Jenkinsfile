pipeline {
  environment {
    registry = "debaduttapradhan1996/shopizer-app"
    registry1 = "debaduttapradhan1996/shopizer-app1"
    registryCredential = 'docker_hub_debadutta'
    dockerImage = ''
    dockerImage1 = ''
  }
  agent any
  stages{
    stage ('Build') {
      steps{
        echo "Building Project"
        sh 'mvn install -DskipTests=true'
	
	      
      }
    }
  
    stage ('Build Docker Image') {
      steps{
        echo "Building Docker Image"
	sh 'cd sm-shop'
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
	  dockerImage1 = docker.build registry1 + ":$BUILD_NUMBER"
        }
      }
    }
    stage ('Push Docker Image') {
      steps{
        echo "Pushing Docker Image"
        script {
          docker.withRegistry( '', registryCredential ) {
              dockerImage.push()
              dockerImage.push('latest')
          }
        }
      }
    }
    stage ('Deploy to Dev') {
      steps{
        echo "Deploying to Dev Environment"
        sh "docker rm -f petclinic || true"
        sh "docker run -d --name=petclinic -p 8081:8080 debaduttapradhan1996/shopizer-app"
      }
    }
  }
}
