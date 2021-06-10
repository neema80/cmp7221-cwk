pipeline {
    agent any
    stages {
        stage('01. SCM dev branch checkout') {
            steps{
                ansiColor('xterm') {
                    git url: "git@github.com:neema80/cmp7221-cwk.git", credentialsId: 'jenkins_ssh_key', branch: 'dev'
                }
            }
        }
        stage('02. UNIT TESTING: Playbook 00 Sanity Check') {
            steps{
                ansiColor('xterm') {
                    ansiblePlaybook colorized: true, disableHostKeyChecking: true, forks: 1, installation: 'Ansible', inventory: 'hosts', playbook: '00_cwk_play.yml', extras: '--syntax-check' 
                    ansiblePlaybook colorized: true, disableHostKeyChecking: true, forks: 1, installation: 'Ansible', inventory: 'hosts', playbook: '00_cwk_play.yml', extras: '--check'
                }
            }
        }
        stage('03. GNS3 APPLICATION') {
            steps{
                ansiColor('xterm') {
                    ansiblePlaybook colorized: true, disableHostKeyChecking: true, forks: 1, installation: 'Ansible', inventory: 'hosts', playbook: '00_cwk_play.yml' }
            }
        }
        stage('04. INTEGRATION TESTING: Playbook 01') {
            steps{
                ansiColor('xterm') {
                    ansiblePlaybook colorized: true, disableHostKeyChecking: true, forks: 1, installation: 'Ansible', inventory: 'hosts', playbook: '01_test.yml' }
            }
        }
        stage('05. DELIVERY: Merge Main branch') {
            steps{
                ansiColor('xterm') {
                    sh '''
                        git config user.name "Nima Bahramzadeh"
                        git config user.email "neema80@gmail.com"
                        git checkout main
                        git pull
                        git remote -v
                        git merge dev main
                        git push --set-upstream origin main
                        git status
                    '''}
            }
        }
    }
}
