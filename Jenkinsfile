node {
    stage('Clone Repository') {
        checkout scm
    }

    stage('Build') {
        sh 'docker run --rm -v $(pwd):/app -w /app node:lts-buster-slim npm install'
    }

    stage('Test') {
        sh 'docker run --rm -v $(pwd):/app -w /app -e CI=true node:lts-buster-slim npm test -- --watchAll=false'
    }
}
