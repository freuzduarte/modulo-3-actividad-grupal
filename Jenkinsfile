pipeline {
    agent any
        stages {
            stage('Comenando el Proyecto') {
                steps {
                    script {
                        echo 'Comenzando el Proyecto'
                    }
                }
            }
            stage('Test') {
                steps {
                // sh 'mvn clean package'
                }
            }
        // stage('Publish to Nexus Repository Manager') {
        //     steps {
        //         script {
        //             pom = readMavenPom file: 'pom.xml'
        //             filesByGlob = findFiles(glob: "target/*.${pom.packaging}")
        //             echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
        //             artifactPath = filesByGlob[0].path
        //             artifactExists = fileExists artifactPath
        //             if (artifactExists) {
        //                 echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}"
        //                 nexusArtifactUploader(
        //                     nexusVersion: 'nexus3',
        //                     protocol: 'http',
        //                     nexusUrl: '192.168.26.129:8081',
        //                     groupId: pom.groupId,
        //                     version: pom.version,
        //                     repository: 'maven-releases',
        //                     credentialsId: 'admin',
        //                     artifacts: [
        //                         [artifactId: pom.artifactId,
        //                                 classifier: '',
        //                                 file: artifactPath,
        //                                 type: pom.packaging]
        //                     ]
        //                 )
        //             }else {
        //                 error "*** File: ${artifactPath}, could not be found"
        //             }
        //         }
        //     }
        // }
        }
// post {
//     always {
//         script {
//             echo 'Prueba'
//             if (currentBuild.result == 'SUCCESS') {
//                 slackSend(channel: '@U05690FEL7P', message: "Proyecto Creado Perfectamente *${currentBuild.currentResult}:* build ${env.BUILD_NUMBER}, ${env.JOB_NAME}", color: '#00FF04')
//             }else if (currentBuild.result == 'FAILURE') {
//                 slackSend(channel: '@U05690FEL7P', message: "No Finalizado*${currentBuild.currentResult}:* build ${env.BUILD_NUMBER}, ${env.JOB_NAME}", color: '#FF0000')
//             }
//         }
//     }
// }
}
