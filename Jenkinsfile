pipeline {
  agent {
    node {
      label 'master'
    }

  }
    stages {
    stage('Node Install ') {
      steps {
        tool name: 'nodejs', type: 'nodejs'
        sh 'npm install'
      }
    }   

        stage('Test and coverage') {
          steps {
            sh 'npm i -D jest-junit'
            sh 'npm i -D jest-sonar-reporter'
            sh 'npm test -- --ci --testResultsProcessor=jest-sonar-reporter --reporters=jest-junit --reporters=default --coverage --coverageReporters=cobertura --coverageReporters=lcov --coverageReporters=html --watchAll=flase'

          }
        }        


    stage('Coverage & Test Report Publish') {
      steps {
        publishCoverage adapters: [coberturaAdapter('coverage/cobertura-coverage.xml')], sourceFileResolver: sourceFiles('NEVER_STORE')
        junit '*.xml'
      }
    }
 }
}
