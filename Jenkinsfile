node{

def mavenhome=tool name:"maven-3.9.8"

stage('Checkoutcode')
{
git changelog: false, poll: false, url: 'https://github.com/imm-ec-proj-oct-renamed/maven-web-application.git'
}
stage('Build'){
 sh "${mavenhome}/bin/mvn clean package"
}
stage('sonarqubereport'){
 sh "${mavenhome}/bin/mvn clean package sonar:sonar"
}
stage('upload artifacts'){
 sh "${mavenhome}/bin/mvn clean package deploy"
}
stage('deployappintotomcat'){

sshagent(['tomcatserver']) {
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war opc@10.10.2.235:/usr/local/tomcat9/webapps"
}
}
}
