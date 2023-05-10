pipeline {
    agent any
        stages {
        stage('Comenzando') {
            steps {
                echo 'Comenzando el Proyecto'
            }
        }
        //Agregando Sonar, utilizando una variable de entorno llamada "TOKENSONAR"
        stage('Sonarcan') {
             steps {
                 sh '''/var/jenkins_home/sonar-scanner/bin/sonar-scanner \
                 -Dsonar.projectName=prueba-de-todo \
                 -Dsonar.projectKey=prueba-de-todo \
                 -Dsonar.projectVersion=1 \
                 -Dsonar.sources=src/main/java/ \
                 -Dsonar.language=java \
                 -Dsonar.java.binaries=./target/classes \
                 -Dsonar.host.url=http://192.168.26.129:9000/ \
                 -Dsonar.login=${TOKENSONAR}'''
             }
        }
        stage('Build') {
                steps {
                    script {
                        sh 'mvn -B package'
                    }
                }
            }
        stage('Test') {
                steps {
                    script {
                        sh 'mvn clean verify'
                    }
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
