pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/makssvelichko/SP-task4.git', credentialsId: 'access_for_jenkins'
            }
        }
        
        stage('Build') {
            steps {
                script {
                    try {
                        bat '"G:\\programs\\VisualStudio\\2022\\MSBuild\\Current\\Bin\\MSBuild.exe" velichko-test1.sln /p:Configuration=Debug /p:Platform=x64 /m'
                    } catch (Exception e) {
                        echo "Build error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline stopped due to build failure.")
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    try {
                        bat '"F:\\coursework\\lab4\\velichko-test1\\x64\\Debug\\velichko-test1.exe"'
                    } catch (Exception e) {
                        echo "Test error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline stopped due to test execution failure.")
                    }
                }
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
        
        failure {
            echo "Pipeline failed. Check logs to fix the issues."
        }
        
        success {
            echo "Pipeline completed successfully!"
        }
    }
}