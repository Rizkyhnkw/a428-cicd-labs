node {
    docker.image('node:16-buster-slim').withRun('-p 3000:3000') { container ->
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh "chmod +x -R ${env.WORKSPACE}"
            sh './jenkins/scripts/test.sh'
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
            sh './jenkins/scripts/kill.sh'
        }
    }
}
