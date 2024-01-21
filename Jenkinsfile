pipeline {
  agent any
  stages {
    stage('Restore') {
      steps {
        sh 'dotnet restore'
      }
    }

    stage('Build') {
      steps {
        sh 'dotnet build --no-restore'
      }
    }

    stage('Test') {
      steps {
        sh 'dotnet test --no-build'
      }
    }

    stage('Publish') {
      steps {
        sh '''                dotnet publish -c Release -o ./publish &&
zip -r publish.zip ./publish/'''
        archiveArtifacts(artifacts: 'publish.zip', allowEmptyArchive: true)
      }
    }

  }
}