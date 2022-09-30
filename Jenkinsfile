node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github5', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh 'git config user.email poretrithynea@gmail.com'
                        sh 'git config user.name poretrithynea'
                        sh 'cat vue-deployment.yml'
                        sh "sed -i 's+poretrithynea/vueminiproject.*+poretrithynea/vueminiproject:${DOCKERTAG}+g' vue-deployment.yml"
                        sh 'cat vue-deployment.yml'
                        sh 'git add .'
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh 'git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/configuration.git HEAD:main'
                        emailext body: 'I hope it works!', subject: 'Testing', to: 'reportteam168@gmail.com'
      }
    }
  }
 
}
}
