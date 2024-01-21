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
        sh 'sh \'dotnet publish -c Release -o ${WORKSPACE}/publish\''
        sh 'sh \'cd ${WORKSPACE} && zip -r publish.zip publish/\''
        archiveArtifacts(artifacts: '${WORKSPACE}/publish.zip', allowEmptyArchive: true, fingerprint: true)
      }
    }

  }
}