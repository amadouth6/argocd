node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email amadouth6@gmail.com"
                        sh "git config user.name amadouth6"
                        //sh "git switch master"
                        sh "cat swh-graphql/myvalues.yaml"
                        sh "sed -i 's+version:.*+version: \"${DOCKERTAG}\"+g' swh-graphql/myvalues.yaml"
                        //sh "sed -i 's+amadouth/graphql.*+amadouth/graphql:${DOCKERTAG}+g' swh-graphql/myvalues.yaml"
                        sh "cat swh-graphql/myvalues.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argocd.git HEAD:master"
      }
    }
  }
}
}
