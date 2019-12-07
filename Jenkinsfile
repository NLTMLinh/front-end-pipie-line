pipeline{
    agent any
    stages{
        stage('Install'){
            steps{
                bat 'npm install'
            }
        }
        stage('Test'){
            steps{
                bat 'npm test -- --no-watch'
            }
        }
        stage('Build'){
            steps{
                bat 'npm run build'
            }
        }
        stage('Deploy') {
          steps{
          
          withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'heroku-git-login',
           usernameVariable: 'admin', passwordVariable: 'admin']]) {
                bat "git push -f https://git.heroku.com/kubo-front-end-ci-cd.git HEAD:master"
          }
          }
          }
    }
    post {
         always {
                mail to: 'tgdd.lelinh@gmail.com',
                subject: 'Demo CI/CD with Jenkins pipeline',
                body: 'Project was built'
        }
        // sucess {
        //     mail to: 'sofiaandyalikesi@gmail.com',
        //         subject: 'Demo CI/CD with Jenkins pipeline',
        //         body: 'Project was built'
        // }
    }
}