node
{
 def mavenHome = tool name: "maven3.9.3"
 stage('CheckoutCode')
{
 git branch: 'master', credentialsId: '72f3fd61-4ced-46e1-b45a-486a061163a4', url: 'https://github.com/Jyothik14/maven-web-application.git'
}
 stage('Build'){
 sh "${mavenHome}/bin/mvn clean package"
}
 stage('ExecuteSonarQubeReport'){
 sh "${mavenHome}/bin/mvn clean sonar:sonar"
}
 stage('UploadArtifactIntoNexus'){
 sh "${mavenHome}/bin/mvn clean deploy"
}
 stage('DeployAppintoTomcat'){
 sshagent(['643c67da-b822-4e15-9969-cca65cad483b']) {
     sh "scp -o StrictHostKeyChecking=no target/maven-wed-application.war ec2-user@50.16.124.99:/opt/apache-tomcat-9.0.78/webapps/"
}
}
}
