pipeline{

    agent{
        kubernetes{
            yamlFile 'pod.yaml'
        }
    }
    stages{
        
        stage('Checkout') {
      steps {
        script {
            
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [ url: 'https://github.com/Vivek-Kornepalli/deployment_manifests.git']])
                
           
//            git  url: 'https://github.com/aakashsehgal/FMU.git'
           // Do a ls -lart to view all the files are cloned. It will be clonned. This is just for you to be sure about it.
           sh "ls -lart ./*" 
          
          }
       }
    }
    stage('Building and pushing using kaniko'){
        steps{
            container('kaniko'){
                script{
                    sh """
                    /kaniki/executor --dockerfile 'pwd'/DockerFile\
                    --context 'pwd'\
                    --destination=registry.digitalocean.com/metaphy/testkaniko"""
                }
            }
        }
    }}
     
}
