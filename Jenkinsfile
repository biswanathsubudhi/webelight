pipeline {
  agent any
  tools {
     nodejs 'node'
  }
    //stage('Project from Git') {
      //steps {
        //git credentialsId: 'git_cred', poll: false, url: 'https://github.com/biswanathsubudhi/webelight.git'
      //}
    //} 
    
    //stage('Build') {
      //steps {
        //sh 'npm build'
      //}
    //}
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }  
  stage('Deploy to Tomcat') {
      steps {
        sshagent(['tomcat']) {
        sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/webelight ec2-user@172.31.36.182:/home/ec2-user/tomcat9/webapps'
        sh 'ssh ec2-user@172.31.36.182 /home/ec2-user/tomcat9/bin/shutdown.sh'
        sh 'ssh ec2-user@172.31.36.182 /home/ec2-user/tomcat9/bin/startup.sh'
        }
      }
    }
  }
}
