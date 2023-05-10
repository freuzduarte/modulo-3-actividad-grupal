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
                 -Dsonar.projectName=actividad-grupal-grupo4 \
                 -Dsonar.projectKey=actividad-grupal-grupo4 \
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
        stage('Publicando el artefacto en NEXUS') {
            steps {
                script {
                    pom = readMavenPom file: 'pom.xml'
                    filesByGlob = findFiles(glob: "target/.${pom.packaging}")
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path
                    artifactExists = fileExists artifactPath
                    if (artifactExists) {
                        echo "** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}"
                        nexusArtifactUploader(
                            nexusVersion: 'nexus3',
                            protocol: 'https',
                            nexusUrl: 'b405-179-60-65-173.ngrok-free.app',
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: 'actividadgrupal',
                            credentialsId: 'adminnexuspatricio',
                            artifacts: [
                                [artifactId: pom.artifactId,
                                        classifier: '',
                                        file: artifactPath,
                                        type: pom.packaging]
                            ]
                        )
                    } else {
                        error "*** File: ${artifactPath}, could not be found"
                    }
                }
            }
        }    
        }
    post {
        failure {
            script {
                echo 'Esto es un mensaje de fallo'
                slackSend(channel: '#actividad-grupal-jenkinsfile', message: " Fallo al compilar proyecto 😢*${currentBuild.currentResult}:* build ${env.BUILD_NUMBER}, ${env.JOB_NAME}", color: '#ff0000')
            }
        }
    }
}
