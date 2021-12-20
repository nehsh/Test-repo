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
     // stage('Quality Analysis') {
        //steps
        //{
          //sh "mvn sonar:sonar"
        //}
      //}
    }
  }

  
