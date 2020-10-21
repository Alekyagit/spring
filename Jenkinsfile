pipeline {
    agent any
    environment
     {
        VERSION = "${BUILD_NUMBER}"
        PROJECT = 'nodeapp'
        IMAGE = "$PROJECT:$VERSION"
        registry = "madavi/spring"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
     
    stages {
      stage('checkout') {
           steps {
             
                git branch: 'main', url: 'https://github.com/inspired123/output-for-springboot-spring-petclinic.git'
             
          }
        }
      stage('Build') { 
            steps {
                sh 'mvn clean package' 
            }
        }  
      stage('Image Build'){
           steps{
               script{
                     dockerImage = docker.build registry + ":$BUILD_NUMBER"
                 }
             }
         }
      stage('Deploy our image') {
          steps{
            script {
              docker.withRegistry( '', registryCredential ) {
              dockerImage.push()
            }
        }
            }
        }
}
} 
