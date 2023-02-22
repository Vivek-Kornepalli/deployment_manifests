// pipeline{

//     agent{

//         lable Built-In Node
        
//     }

    
//   podTemplate(yaml: '''
//               kind: Pod
//               spec:
//                 containers:
//                 - name: kaniko
//                   image: gcr.io/kaniko-project/executor:v1.6.0-debug
//                   imagePullPolicy: Always
//                   command:
//                   - sleep
//                   args:
//                   - 99d
//                   volumeMounts:
//                     - name: jenkins-docker-cfg
//                       mountPath: /kaniko/.docker
//                 volumes:
//                 - name: jenkins-docker-cfg
//                   projected:
//                     sources:
//                     - secret:
//                         name: regcred
//                         items:
//                           - key: .dockerconfigjson
//                             path: config.json
// '''
//   ) {
//     stages{
        
//         stage('Checkout') {
//       steps {
//         script {
            
//             checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [ url: 'https://github.com/Vivek-Kornepalli/deployment_manifests.git']])
                
           
// //            git  url: 'https://github.com/aakashsehgal/FMU.git'
//            // Do a ls -lart to view all the files are cloned. It will be clonned. This is just for you to be sure about it.
//            sh "ls -lart ./*" 
          
//           }
//        }
//     }
//     stage('Building and pushing using kaniko'){
//         steps{
//             container('kaniko'){
//                 script{
//                     sh """
//                     /kaniki/executor --dockerfile 'pwd'/DockerFile\
//                     --context 'pwd'\
//                     --destination=registry.digitalocean.com/metaphy/testkaniko"""
//                 }
//             }
//         }
//     }}
     
// }
// }

























pipeline {
    agent {
        kubernetes {
            // Use the Kaniko image from GCR
            yaml """
            apiVersion: v1
            kind: Pod
            metadata:
              labels:
                app: kaniko
            spec:
              containers:
              - name: kaniko
                image: gcr.io/kaniko-project/executor:latest
                // args: ["--dockerfile=<DOCKERFILE_PATH>",
                //         "--context=<CONTEXT_PATH>",
                //         "--destination=registry.digitalocean.com/metaphy/<IMAGE_NAME>:<TAG>",
                //         "--insecure"]
                volumeMounts:
                - name: kaniko-secret
                  mountPath: /kaniko/.docker
                  readOnly: true
                imagePullSecrets:
                - name: regcred
              volumes:
              - name: kaniko-secret
                secret:
                  secretName: kaniko-secret
            """
        }
    }
    stages {
        stage('Clone repository') {
            steps {
                // Clone the repository
                git branch: 'main',
                    url: 'https://github.com/Vivek-Kornepalli/deployment_manifests.git'
            }
        }
        stage('Build and deploy image') {
            steps {
                // Build and deploy the Docker image using Kaniko
                sh """
                /kaniko/executor --dockerfile 'pwd'/DockerFile \
                --context 'pwd' \
                --destination=registry.digitalocean.com/metaphy/testkaniko"
                """
                
            }
        }
    }
}
