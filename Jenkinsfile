node('jenkins-slave') {

    agent{
        kubernetes{
            yamlFile ''
        }
    }
    stages{
        
        stage('test pipeline') {
        sh(script: """
            echo "hello" """)
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
