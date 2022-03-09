pipeline{

agent any

tools{
 maven "maven"
}


options{
timestamps()
buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5'))

}

stages{
  stage('CheckOut thecode'){
  steps{
  git branch: 'devfeb', credentialsId: '0825bb6c-cdd6-4885-82ea-f41445e2b7bb', url: 'https://github.com/dsfsandeep9/maven-web-application.git'
     }
     }

 stage('Build'){
  steps{
  sh "mvn clean package"
   }
  }
  
  stage('Sonar'){
  steps{
  sh "mvn clean package sonar:sonar"
   }
  }
 
 stage('Deploy to Tomcat'){
  steps{
  sshagent(['533101e5-0106-4c0e-b00f-4f6b95d6c1bc']){
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@54.221.68.65:/opt/apache-tomcat-9.0.58/webapps/"
    }
   }
   }
   
}
}
