pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh '''
                    echo "Running build script..."
                    chmod +x build.sh
                    ./build.sh
                '''
            }
        }
    }

    post {
        success {
            emailext (
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Build Status: SUCCESS
Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}

Console Output:
${env.BUILD_URL}console
""",
                to: "udhayakumarethiraj@gmail.com"
            )
        }
        failure {
            emailext (
                subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Build Status: FAILED
Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}

Check logs:
${env.BUILD_URL}console
""",
                to: "udhayakumarethiraj@gmail.com"
            )
        }
    }
}
