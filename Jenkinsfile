node {
    def app

    stage('Build') {
        checkout scm
        app = docker.build("react-app")
    }

    stage('Test') {
        app.inside {
            sh 'echo "Running tests..."'
            sh 'CI=true npm test -- --watchAll=false'
        }
    }

    stage('Manual Approval') {
        input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
    }

    stage('Deploy') {
        app.inside('-p 3000:3000') {
            sh 'serve -s build -l 3000 &'
            echo 'Aplikasi berjalan selama 1 menit...'
            sleep(time: 60, unit: 'SECONDS')
            echo 'Selesai!'
        }
    }
}
