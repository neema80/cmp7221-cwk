pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps{
                ansiColor('xterm') {
                    git url: "git@github.com:neema80/cmp7221-cwk.git", credentialsId: 'jenkins_ssh_key', branch: 'dev'
                }
            }
        }
        stage('Test Ansible Playbook') {
            steps{
                ansiColor('xterm') {
                    ansiblePlaybook colorized: true, disableHostKeyChecking: true, forks: 1, installation: 'Ansible', inventory: 'hosts', playbook: '00_cwk_play.yml'                }
            }
        }
        stage('Build') {
            steps{
                ansiColor('xterm') {
                    sh '''
                        git config user.name "Nima Bahramzadeh"
                        git config user.email "neema80@gmail.com"
                        git checkout main
                        git remote -v
                        git merge dev main
                        git push --set-upstream origin main
                        git status
                    '''}
            }
        }
    }
}
