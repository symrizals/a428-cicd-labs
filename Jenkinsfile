node {
    stage('Clone Repository') {
        checkout scm
    }

    stage('Build') {
        sh 'docker build -t react-app .'
    }

    stage('Test') {
        sh 'docker run --rm react-app sh -c "CI=true npm test -- --watchAll=false"'
    }
}
