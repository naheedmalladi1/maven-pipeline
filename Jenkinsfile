pipeline
{
agent any 
stages
{
 stage('scm checkout')
 { steps { git branch: 'master', url: 'https://github.com/prakashk0301/mavenproject' }}


 stage('compile source code')
 { steps {withMaven(jdk: 'LocalJDK', maven: 'LocalMaven') {
  sh 'mvn compile'
   }
         }
 }


 stage('build source code')
 { steps { withMaven(jdk: 'LocalJDK', maven: 'LocalMaven'){
  sh 'mvn package'
  
   }
 }
}

 stage('deploy to tomcat server-Dev-Automated')
  {steps { sshagent(['deploy-to-tomcat']) 
   {
    sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.9.183:/var/lib/tomcat/webapps'
   }
         }
  }
}
}
