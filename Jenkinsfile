pipeline {
    agent any
        stages {
        stage('Comenzando') {
            steps {
                echo 'Comenzando el Proyecto'
            }
        }
        }
    post {
        failure {
            script {
                echo 'Esto es un mensaje de fallo'
                slackSend(channel: '#actividad-grupal-jenkinsfile', message: " Proyecto Creado Perfectamente *${currentBuild.currentResult}:* build ${env.BUILD_NUMBER}, ${env.JOB_NAME}", color: '#00FF04')
            }
        }
    }
}
