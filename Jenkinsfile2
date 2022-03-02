pipeline {
    agent any

    stages {
        stage('NPM Build') {
          steps {
            sh "echo 'we are in'"
          }
        }
        stage('push'){
            steps{
                
//                 git(
//                    url: 'git@github.com:KHEfreiIntervenant/Jenkins_test.git',
//                    credentialsId: 'github-pushes',
//                    branch: "main"
//                 )
                
//                 withCredentials([gitUsernamePassword(credentialsId: 'github-credentials',
//                  gitToolName: 'git-tool')]) {
//                   sh 'if [ ! `git branch --list release` ]; then git branch release; fi'
//                     sh 'git checkout release'
//                     sh 'git push origin release'
//                 }
                sshagent(['github-pushes']) {
//                     sh 'git checkout main'
//                     sh 'git add *'
//                     sh 'git commit -m "test commit"'
//                       sh "git push origin HEAD:main"
                    sh '''
                    if [ ! `git branch --list release` ]
                  then git branch release
                  fi
                  
                  git checkout release
                  git add *
                  git commit -m "test commit"
                  git commit --allow-empty -m "test withCredentials"
                  git push -f origin release
                    '''
                }
            }
        }
        stage('push again'){
            steps{
                withCredentials([sshUserPrivateKey(credentialsId: 'github-pushes',keyFileVariable: 'SSH_KEY')]) {
                  sh '''
                  git remote set-url origin git@github.com:KHEfreiIntervenant/Jenkins_test.git
                  git config user.name KHEfreiIntervenant
                  git config user.email khodor.hammoud@intervenantes.efrei.net
                  GIT_SSH_COMMAND="ssh -i $SSH_KEY"
                  if [ ! `git branch --list release` ]
                  then git branch release
                  fi
                  git checkout release
                  git commit --allow-empty -m "test withCredentials"
                  git push origin release
                  '''
                }
//                 withCredentials([usernamePassword(credentialsId: 'github-pushes')]) {
//                         sh "git branch release"
//                         sh "git push https://github.com/KHEfreiIntervenant/Jenkins_test release"
//                         sh('git push https://github.com/KHEfreiIntervenant/Jenkins_test')
//                     }
            }
        }
    } 
}
