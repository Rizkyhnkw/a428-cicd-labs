node {
    docker.image('node:16-buster-slim').inside('-p 3001:3000') {
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh "chmod +x -R ${env.WORKSPACE}"
            sh './jenkins/scripts/test.sh'
        }
         stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
            sh 'sleep 60'
            sh './jenkins/scripts/kill.sh'
        }
    }
}
