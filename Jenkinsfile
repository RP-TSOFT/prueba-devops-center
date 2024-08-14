pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/RP-TSOFT/prueba-devops-center'
            }
        }
        stage('PMD Analysis') {
            steps {
                sh 'pmd -d ./src -R rulesets/java/basic.xml -f html -r pmd-report.html'
            }
        }
        stage('Publish PMD Report') {
            steps {
                publishHtml(target: [
                    reportName: 'PMD Analysis',
                    reportDir: '.',
                    reportFiles: 'pmd-report.html'
                ])
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'pmd-report.html', allowEmptyArchive: true
        }
    }
}
