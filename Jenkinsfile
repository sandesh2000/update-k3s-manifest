node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email sandesh174@gmail.com"
                        sh "git config user.name sandesh2000"
                        //sh "git switch master"
                        sh "cat manifest.yaml"
                        sh "sed -i 's+sandesh2000/k3s-php-jenkins.*+sandesh2000/k3s-php-jenkins:${DOCKERTAG}+g' manifest.yaml"
                        sh "cat manifest.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/update-k3s-manifest.git HEAD:master"
      }
    }
  }
}
}