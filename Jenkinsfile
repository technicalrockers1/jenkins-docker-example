pipeline {
    agent any
    tools {
        maven 'MAVEN'
    }
    stages {
        stage('Build Maven') {
           steps {
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '4938c1db-dcd0-4b46-bffb-11e50ab421c5', url: 'https://github.com/technicalrockers1/jenkins-docker-example.git']])
               sh "mvn -Dmaven.test.failure.ignore=true clean package"
           }
        }
        stage ('build Docker Image') {
            steps {
                script {
                    sh 'docker build -t technicalrockers1/my-app-1.0 .'
                }
            }
        }
        stage ('push Docker Image') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u Nadeemshah -p $(dockerhubpwd)'
}               
                    sh 'docker push technicalrockers1/my-app-1.0'
                }
            }
            
        }
    }
}
