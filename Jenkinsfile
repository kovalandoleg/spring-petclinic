pipeline {
  agent { label 'ubuntu-1604' }
  tools {
    maven 'M3'
  }
  stages {
    stage('Preparation') {
      steps {
        git 'https://github.com/kovalandoleg/spring-petclinic.git'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean'
        sh 'mvn package'
      }
    }
    stage('Tests') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Artifacts') {
      steps {
        googleStorageBuildLogUpload bucket: "gs://test-temp-project-667-id-jenkins-artifacts/$JOB_NAME/$BUILD_NUMBER", credentialsId: 'test-temp-project-667-id', logName: 'build-log.txt'
        googleStorageUpload bucket: "gs://test-temp-project-667-id-jenkins-artifacts/$JOB_NAME/$BUILD_NUMBER", credentialsId: 'test-temp-project-667-id', pattern: '**/target/*.jar'
      }
    }
  }
}
