pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps{
                ansiColor('xterm') {
                    git branch: 'main', changelog: false, credentialsId: 'neema80', poll: false, url: 'https://github.com/neema80/cmp7221-cwk'
                    git branch: 'dev', changelog: false, credentialsId: 'neema80', poll: false, url: 'https://github.com/neema80/cmp7221-cwk'
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
                        git checkout main
                        git merge dev main
                        git push
                        git status
                    '''}
            }
        }
    }
}
