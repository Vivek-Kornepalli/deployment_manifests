def label = "kube-agent"
podTemplate(label: label, 
containers: [
                            containerTemplate(
                                name: 'kaniko',
                                image: 'gcr.io/kaniko-project/executor:v1.6.0-debug',
                                command: 'sleep',
                                args: '99d',
                                ttyEnabled: true
                            )
                        ],
                        volumes: [
                            secretVolume(
                                secretName: 'regcred',
                                mountPath: '/kaniko/.docker'
                            )
                        ])

// podTemplate
// (
//   yaml '''
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
// )
{
 node(label) {
   stage('Stage 1: Build with Kaniko'){

     container('kaniko'){
       sh '''
       sleep 30
       /kaniko/executor --force -f Dockerfile --context=git://github.com/Vivek-Kornepalli/deployment_manifests.git \
               --destination=registry.digitalocean.com/metaphy:latest \
               --insecure \
               --skip-tls-verify  \
               -v=debug
          '''
     }
   }
 }
}

// pipeline {
//     agent {lable: "kube-agent"}
//     stages {
//         stage('Clone repository') {
//             steps {
//                 // Clone the GitHub repository to the workspace
//                 git branch: 'main', url: 'https://github.com/Vivek-Kornepalli/deployment_manifests.git'
//             }
//         }
//         stage('Build Docker image') {
//             steps {
//                 // Run the Kaniko container to build the Docker imag
//                 container('kaniko') {
//                     sh '/kaniko/executor --dockerfile=${WORKSPACE}/Dockerfile --context=dir://workspace --destination=registry.digitalocean.com/metaphy:latest'
//                 }
//             }
//         }
        
//     }
// }
