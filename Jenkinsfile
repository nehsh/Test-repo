pipeline {
  agent any {
    stages {
      stage ('code checkout'){
        steps {
          git branch: '', 
          credentialsId: 'ebbe7111-1a36-42b2-97b3-ff97f0092dbf', 
          url: 'https://github.com/nehsh/Test-repo.git'
        }
      }
    }
  }
}
  
