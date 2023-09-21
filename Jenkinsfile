pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    parameters {
        string defaultValue: '100.26.235.195', name: 'tomcat-server'
    }
    stages{
        
        stage('checkout'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/MayuriTalhar/jenkins_tomcat_demo.git']])
            }    
        }
        stage('Build'){
            steps{
                echo 'Building Maven project'
                bat 'mvn clean install'
            }
        }
        stage('Deploy on Tomcat'){
            steps{
                echo 'Deploying on Tomcat '
                withCredentials([sshUserPrivateKey(credentialsId: 'tomcat-cred', keyFileVariable: 'SSH_KEY', passphraseVariable: '', usernameVariable: 'TOMCAT_USER')]) {
                    bat 'scp -v -o StrictHostKeyChecking=no target/demowar-0.0.1-SNAPSHOT.war ubuntu@54.89.205.78::/opt/tomcat/webapps'
                }
            }
        }
        
    }
        

}
