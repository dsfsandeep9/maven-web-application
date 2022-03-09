pipeline{

agent any

tools{
 maven "maven"
}

options{
timestamps()
buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5'))
}

/*
agent{
label "nodename"
}
*/

stages{
 stage('CheckOutCode')
 {
  steps{
  git branch: 'dev2', credentialsId: '64844fdb-146d-4a9d-9d8e-89be04654948', url: 'https://github.com/dsfsandeep9/maven-web-application.git'
   }
 }
  stage('Build'){
  steps{
  sh "mvn clean package"
   }
  }

  stage('SonarQube'){
  steps{
  sh "mvn clean sonar:sonar"
   }
  }

  stage('Nexus'){
  steps{
  sh "mvn clean deploy"
   }
  }

 stage('Deploy to Tomcat'){
  steps{
  sshagent(['68010eb2-f56e-4c00-a634-cde746671bc8']){
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@54.160.240.13:/opt/apache-tomcat-9.0.58/webapps/"
    }
   }
   }
  
 }
 
 post{

 always{
 emailext body: 'Build is Over', subject: 'Build Over', to: 'dsf.sandeep@gmail.com'

 }

 success{
 emailext body: 'Build is Over - success', subject: 'Build Over', to: 'dsf.sandeep@gmail.com'
 }

 failure{
  emailext body: 'Build is Over - failed', subject: 'Build Over', to: 'dsf.sandeep@gmail.com'

  }  

}
}
