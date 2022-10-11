pipeline {
  agent any
    stages {
      stage('Build') {
            steps {
                nodejs(nodeJSInstallationName: 'Node 12.22.12', configId: '<config-file-provider-id>') {
                    sh 'npm config ls'
                }
            }
      }
        stage('Code Analysis') {
          environment {
    SCANNER_HOME = tool 'SonarScanner'
    PROJECT_NAME = "ChatApp"
  }
  steps {
    withSonarQubeEnv('SonarQube Server') {
        sh '''$SCANNER_HOME/bin/sonar-scanner 
           '''
    }
  }
 }
    
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') { 
                  
                  waitForQualityGate abortPipeline: true
                }
            }
        }

    
  }
}
