pipeline {
  agent any
  tools{
    maven 'maven-3.5.2'
       }
    stages {
      stage ('code checkout'){
        steps {
          echo "fetching code from master branch...."
          git branch: 'dev', 
          credentialsId: 'ebbe7111-1a36-42b2-97b3-ff97f0092dbf', 
          url: 'https://github.com/nehsh/Test-repo.git'
        }
      }
      
      stage('Maven Version'){
        steps{
          echo "Hello, Maven"
          sh "mvn --version"
        }
      }
      stage('Maven Install'){
        steps{
          echo "compiling the code"
          sh "mvn clean install"
        }
      }
      
      stage('Sonar Scan') {
        steps {
          withSonarQubeEnv(installationName: 'sonar1') { 
              sh "mvn clean sonar:sonar"
            }
              }
         }
          
      stage('Upload War To Nexus'){
            steps{
                //script{
                    //pom = readFile file: "pom.xml";
                    //filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    //artifactPath = filesByGlob[0].path;
                    //echo "connecting to Nexus"
                    //def mavenPom = readFile file: 'pom.xml'
                    //def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "hello_world-snapshots" : "hello_world-release"
                    nexusArtifactUploader artifacts:[[artifactId: 'hello_world', 
                      classifier: '', 
                      file: '/var/jenkins_home/.m2/repository/com/mycompany/hello_world/1.0.0-SNAPSHOT/hello_world-1.0.0-SNAPSHOT-mule-application.jar', 
                      type: 'mule-application']],
                      credentialsId: 'bbb2026f-8763-4091-a5b9-b029d602d093', 
                      groupId: 'com.mycompany', 
                      nexusUrl: '35.200.199.182', 
                      nexusVersion: 'nexus3', 
                      protocol: 'http', 
                      repository: 'Hello-world_snapshot', 
                      version: "1.0.0-SNAPSHOT"                                      
            }
        }
      //stage('deploy to Exchange'){
        //steps{
          //withCredentials([usernamePassword(credentialsId: 'anypoint', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
          //sh "mvn clean deploy -Pexchange -Danypoint.username=USERNAME -Danypoint.password=PASSWORD" 
          //}
        //}
      //}
      stage('download from nexus'){
        steps{
          withCredentials([usernamePassword(credentialsId: 'bbb2026f-8763-4091-a5b9-b029d602d093', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]){
          sh 'curl -u $USERNAME:$PASSWORD  http://35.200.199.182/repository/Hello-world_snapshot/com/mycompany/hello_world/1.0.0-SNAPSHOT/hello_world-1.0.0-20211229.065117-6.mule-application --output mule-application.jar'
          sh 'ls -lrta' 
          echo "downloading from nexus"
          sh 'pwd'
          sh 'hostname'
          }}}
      
      stage('deploy to cloudhub'){
                
      steps{
        withCredentials([usernamePassword(credentialsId: 'anypoint', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
          
          sh 'ls'
          //sh "cd /var/jenkins_home/workspace/;mvn deploy -pcloudhub"}}}
          //sh "mvn clean deploy -DmuleDeploy -Dmule.env=DEV -Dcloudhub.workers=1 -Dcloudhub.worker.type=MICRO -Dcloudhub.region=us-east-2 -Durl=https://anypoint.mulesoft.com -Dartifact.path=./mule-application.jar"
          sh "mvn clean deploy -DmuleDeploy"}
      }}
    }
  }

  
