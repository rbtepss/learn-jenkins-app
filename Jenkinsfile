pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                    echo "Test stage"
                    🤩test -f build/index.html
                    if [ -f build/index.html ]; then
                        echo "✅ index.html found"
                    else
                        echo "❌ index.html NOT found"
                        exit 1
                    fi
                '''
            }
        }
    }
}