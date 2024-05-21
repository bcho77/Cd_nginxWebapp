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
                    withCredentials([usernamePassword(credentialsId: 'GITHUB_CREDENT', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]){
                    sh '''
                    git config user.email temgvan@gmail.com
                    git config user.name bcho77
                    cat deployment.yml
                    yq -i '.image = "vaninoel/carvilla:${env.BUILD_NUMBER}"' deployment.yml
                    cat deployment.yml
                    git add .
                    git commit -m 'update deployment.yml manifest: ${env.BUILD_NUMBER}'
                    git push https://$GIT_USERNAME:$GIT_PASSWORD@github.com/bcho77/Cd_nginxWebapp.git HEAD:main
                    '''
                    }
                }             
            }
        }
    }
}