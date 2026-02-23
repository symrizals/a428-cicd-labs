node {
    stage('Build') {
        docker.image('node:lts-buster-slim').inside('-p 3000:3000') {
            checkout scm
            sh 'npm install'
        }
    }

    stage('Test') {
        docker.image('node:lts-buster-slim').inside('-p 3000:3000') {
            checkout scm
            sh 'npm install'
            sh './jenkins/scripts/test.sh'
        }
    }

    stage('Manual Approval') {
        input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
    }

    stage('Deploy') {
        docker.image('node:lts-buster-slim').inside('-p 3000:3000') {
            checkout scm
            sh 'npm install'
            sh './jenkins/scripts/deliver.sh'
            echo 'Aplikasi berjalan selama 1 menit...'
            sleep(time: 60, unit: 'SECONDS')
            sh './jenkins/scripts/kill.sh'
            echo 'Selesai!'
        }
    }
}
