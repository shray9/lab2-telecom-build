pipeline {
    agent {
        label 'docker-agent-1'
    }


    stages {

        stage('Checkout') {
            steps {
                echo "📥 Source code checked out from GitHub"
            }
        }

      
        stage('Build') {
            steps {
                echo "🔧 Building telecom microservice"
                sh '''
                    mkdir -p build
                    cp -r src build/
                '''
            }
        }

        stage('Package Artifact') {
            steps {
                script {
                    def artifact = "${APP_NAME}-build-${env.BUILD_NUMBER}.tar.gz"
                    sh "tar -czf ${artifact} build/"
                    env.ARTIFACT_NAME = artifact
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: '*.tar.gz', fingerprint: true
                echo "📦 Artifact archived"
            }
        }
    }

    post {
        success {
            echo "✅ Telecom build successful"
        }
        failure {
            echo "❌ Telecom build failed"
        }
    }
}
