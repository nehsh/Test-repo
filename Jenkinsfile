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
      stage('publish to Nexus repository'){
        steps {
          echo "publish the package to nexus artifactory"
          nexusPublisher nexusInstanceId: 'Nexus', 
          nexusRepositoryId: 'hello_world-release', 
          packages: [[$class: 'MavenPackage', mavenAssetList: [], 
          mavenCoordinate: [artifactId: 'hello_world', groupId: 'com.mycompany', packaging: 'jar', version: '1.0.0']]]
        }
      }
     }
  }

  
