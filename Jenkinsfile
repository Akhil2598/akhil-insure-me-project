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
    
    withCredentials([string(credentialsId: 'dockercred', variable: 'dockercred')]) {
        sh 'sudo docker login -u akhil2598 -p ${dockercred}'
        sh 'sudo docker push akhil2598/insurance-project-image:1.0'
    
}
    }
    stage('ansible-deploy')
    {
    
       ansiblePlaybook become: true, credentialsId: 'ansiblecred', disableHostKeyChecking: true, installation: 'myansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}
