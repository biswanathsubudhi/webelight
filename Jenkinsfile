pipeline {
  agent any
  tools {
     nodejs 'node'
  }
  
  stages {
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }
    stage('Project from Git') {
      steps {
        git credentialsId: 'git_cred', poll: false, url: 'https://github.com/biswanathsubudhi/webelight.git'
      }
    } 
    
    //stage('Build') {
      //steps {
        //sh 'npm build'
      //}
    //}
    stage('Deploy to Tomcat') {
      steps {
        sshagent(['tomcat']) {
        sh 'scp -o StrictHostKeyChecking=no index.js ec2-user@172.31.36.182://tomcat9/webapps'
        sh 'ssh ec2-user@172.31.36.182:/tomcat9/bin/shutdown.sh'
        sh 'ssh ec2-user@172.31.36.182:/tomcat9/bin/startup.sh'
        }
      }
    }
  }
}
