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
        sh '''dotnet publish --no-build -o ./publish
'''
        sh 'sh \'zip -r publish.zip ${WORKSPACE}/publish/\''
        archiveArtifacts(artifacts: './publish.zip', allowEmptyArchive: true, fingerprint: true)
      }
    }

  }
}