node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernamePassword: 'GIT_USERNAME')])
                sh "git config user.email pedrom7591@gmail.com"
                sh "git config user.name odemira"
                sh "cat deployment.yaml"
                sh "sed -i 's+odemira/test.*+odemira/test:${DOCKERTAG}+g' deployment.yaml"
                sh "cat deployment.yaml"
                sh "git add ."
                sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}"
                sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git"
            }
        }
    }
}