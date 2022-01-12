pipeline {
agent {
label 'build node'
}

stages {

stage ('Checkout') 
{
steps
    {
    
        checkout scm
        
    }
    
}
stage ('build') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/microservice/account-service; mvn clean install" 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/microservice/account-service; sudo docker build -t account-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/microservice/account-service ; sudo  docker login -uakhiladocker12 -palekya@12 "
        sh "cd /home/ubuntu/workspace/microservice/account-service ; sudo docker tag account-service akhiladocker12/dev "
        sh "cd /home/ubuntu/workspace/microservice/account-service ; sudo docker push akhiladocker12/dev "
        
        
    }
}
    
    
stage ('k8sdeployment') 
    {
        steps {
            node (' Ansible-server') {
             sh " sudo ansible-playbook /root/k8s.yaml"
   
    }
}
}
}
    
    
}
