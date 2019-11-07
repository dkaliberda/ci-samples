pipeline {
    agent {
        docker {
            image 'katalonstudio/katalon:6.3.3'
            args "-u root"
        }
    }
    stages {
        stage('Test') {
            steps {
                sh 'katalon-execute.sh -browserType="Chrome" -retry=0 -statusDelay=15 -testSuitePath="Test Suites/TS_RegressionTest"'
                script {
                    def testResults = findFiles(glob: 'build/reports/**/*.xml')
                    for(xml in testResults) {
                        touch xml.getPath()
                    }
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'report/**/*.*', fingerprint: true
            junit 'report/**/JUnit_Report.xml'
        }
    }
}
