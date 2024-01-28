pipeline {
    agent any

    environment {
        DOCKERTAG = "latest" // Add your default DOCKERTAG here
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Update GIT') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                            sh "git config user.email chnarsimha2580@gmail.com"
                            sh "git config user.name Narsi12"
                            sh "cat deployment.yaml"
                            sh "sed -i 's+narsimha2580/test.*+narsimha2580/test:${DOCKERTAG}+g' deployment.yaml"
                            sh "cat deployment.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
                        }
                    }
                }
            }
        }
    }
}
