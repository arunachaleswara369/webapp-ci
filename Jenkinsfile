pipeline {
  agent any
  tools {
    maven 'maven3'
    jdk 'JDK8'
  }
  stages {
    stage('Build maven') {
      steps {
        bat 'cd'
        bat 'mvn clean install package'
      }
    }
    stage('Copy Artifact') {
      steps {
        bat 'cd'
	bat 'del docker\\spring-petclinic-2.2.0.BUILD-SNAPSHOT.jar'
        bat 'xcopy /S target\\*.jar docker\\'
      }
    }
    stage('Build docker image') {
      steps {
        script {
          def customImage = docker.build('arunachaleswara369/petclinic', "./docker")
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            customImage.push("${env.BUILD_NUMBER}")
          }
        }
      }
    }
  }
}
