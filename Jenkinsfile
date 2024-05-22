pipeline {
    agent any

    stages {
        stage('Checkout from SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/bcho77/Cd_nginxWebapp.git'
            }
        }

        stage('Update Git with New Build Number') {
            steps {
                script {
                    def buildNumber = params.BUILD_NUMBER
                    
                    withCredentials([usernamePassword(credentialsId: 'GITHUB_CREDENT', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh """
                        git config user.email "temgvan@gmail.com"
                        git config user.name "bcho77"
                        cat deployment.yml
                        sed -i 's+vaninoel/carvilla.*+vaninoel/carvilla:${buildNumber}+g' deployment.yml
                        cat deployment.yml
                        git add .
                        git commit -m 'Update deployment.yml manifest: ${buildNumber}'
                        git push https://$GIT_USERNAME:$GIT_PASSWORD@github.com/bcho77/Cd_nginxWebapp.git HEAD:main
                        """
                    }
                }
            }
        }
    }
}
