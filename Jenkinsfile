// def label = "kube-agent"
// podTemplate(label: label, containers:[
//  containerTemplate(name: 'kaniko', image: 'gcr.io/kaniko-project/executor:debug', command: '/busybox/cat', ttyEnabled: true)
// ]){
//  node(label) {
//    stage('Stage 1: Build with Kaniko'){
//      container('kaniko'){
//        sh '/kaniko/executor -f Dockerfile --context=git://github.com/Vivek-Kornepalli/deployment_manifests.git \
//                --destination=registry.digitalocean.com/metaphy:latest \
//                --insecure \
//                --skip-tls-verify  \
//                -v=debug'
//      }
//    }
//  }
// }

pipeline {
    agent any
    stages {
        stage('Clone repository') {
            steps {
                // Clone the GitHub repository to the workspace
                git branch: 'main', url: 'https://github.com/Vivek-Kornepalli/deployment_manifests.git'
            }
        }
        stage('Build Docker image') {
            steps {
                // Run the Kaniko container to build the Docker imag
                container('kaniko') {
                    sh '/kaniko/executor --dockerfile=${WORKSPACE}/Dockerfile --context=dir://workspace --destination=registry.digitalocean.com/metaphy:latest'
                }
            }
        }
        
    }
}
