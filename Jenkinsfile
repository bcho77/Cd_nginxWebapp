pipeline{
    agent any

    stages{
        
        stage('check out for scm'){
            steps{
                git branch: 'main',
                url: 'https://github.com/bcho77/Cd_nginxWebapp.git'

            }
        }
        stage('Updating Git with the new build number '){
            steps{

                 script{
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
                        withCredentials([usernamePassword(credentialsId: 'GITHUB_CREDENT', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')])
                        sh "git config user.email temgvan@gmail.com"
                        sh "git config user.name bcho77"
                        sh "cat deployment.yml"
                        sh "sed -i 's+vaninoel/carvilla.*+vaninoel/carvilla:${BUILD_NUMBER}+g'deployment.yml"
                        sh "cat deployment.yml"
                        sh "git add ."
                        sh "git commit -m 'update deployment.yml manifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/bcho77/Cd_nginxWebapp.git HEAD:main"

                    }             }
            }
        }
    }
}