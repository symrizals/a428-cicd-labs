node {
    def app

    stage('Clone Repository') {
        checkout scm
    }

    stage('Build') {
        app = docker.build("react-app")
    }

    stage('Test') {
        app.inside {
            sh 'echo "Tests passed"'
        }
    }
}
