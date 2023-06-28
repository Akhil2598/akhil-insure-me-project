node{
    stage('git checkout')
    {
        git branch: 'master', url: 'https://github.com/Akhil2598/akhil-insure-me-project.git'
    }

    stage('compile'){
    
    sh 'mvn clean compile'
    }
    stage('test'){
        
    sh 'mvn clean test'
    }
    stage('package'){
        
    sh 'mvn clean package'
    }
    stage('build a docker image')
    {
    sh 'sudo docker build -t akhil2598/insurance-project-image:1.0 .'
   
    }
    stage('push docker image to akhilrepo')
    {
    
    withCredentials([string(credentialsId: 'akhildocker', variable: 'docker')]) {
        sh 'docker login -u akhil2598 -p ${docker}'
        sh 'docker push akhil2598/insurance-project-image:1.0'
    
}
    }
    stage('deploy')
    {
    
       ansiblePlaybook become: true, credentialsId: 'akhilcred', disableHostKeyChecking: true, installation: 'myansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}
