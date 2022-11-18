pipeline {
  agent any
  tools {
    maven 'Maven'
    jdk 'jdk'
  }
  environment {
      dockerImage =''
      registry = 'maradanam/test-app1'
      docker_credentails = 'docker_hub'
  }
  stages {
    stage('git checkout') {
    	steps {
            //	git credentialsId: 'git_hub_certs', url: 'https://github.com/mnaidu10/spring-boot-test'
            checkout([$class: 'GitSCM', branches: [[name: '*/$BRANCH_NAME']], extensions: [], userRemoteConfigs: [[credentialsId: 'git_hub_certs', url: 'https://github.com/mnaidu10/spring-boot-test']]])
    	}
    }
    stage('build') {
    	steps {
            	bat 'mvn install'
    	}
    }
    stage('docker image build') {
        steps {
            script {
                //dockerImage = docker.build registry
                bat 'docker build -t maradanam/spring-boot-test .'
            }
        }
    }
    stage('docker image push') {
        steps {
            script {
                    bat 'docker login -u maradanam -p Dec123!@#'
                    bat 'docker push maradanam/spring-boot-test'
            }
        }
    }
  }
}
