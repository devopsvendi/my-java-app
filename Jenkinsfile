pipeline {
    agent any

    environment {
        MVND_HOME = "/opt/mvnd/bin"
        PATH = "$MVND_HOME:$PATH"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/devopsvendi/my-java-app.git',
                    credentialsId: 'Github'
            }
        }

        stage('Build') {
            steps {
                sh '/opt/mvnd/bin/mvnd clean package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build successful!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
