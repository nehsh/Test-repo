pipeline {
  agent any
  tools{
    maven 'maven-3.5.2'
       }
    stages {
      stage ('code checkout'){
        steps {
          echo "fetching code from master branch...."
          git branch: 'master', 
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
                      file: 'target/hello_world-1.0.0-SNAPSHOT.jar', 
                      type: 'mule-application']],
                      credentialsId: 'bbb2026f-8763-4091-a5b9-b029d602d093', 
                      groupId: 'com.mycompany', 
                      nexusUrl: '35.200.199.182', 
                      nexusVersion: 'nexus3', 
                      protocol: 'http', 
                      repository: 'hello_world-release', 
                      version: "1.0.0-SNAPSHOT"                                      
            }
        }
     }
  }

  
