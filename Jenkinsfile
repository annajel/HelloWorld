node {
    
    parameters {
        string(name: 'TOKEN', defaultValue: 'f2e4c6b2917f453983d77912927a192e87174dfe', description: 'Extented Access Token from platform')
        string(name: 'CONTEXT', defaultValue: 'blueOcean', description: 'Deploy to...')
        string(name: 'TARGET_ENV', defaultValue: 'env-8327338', description: 'Where to deploy?')
        string(name: 'JELASTIC_API_ENDPOINT', defaultValue: 'app.madrid.central.jelastic.team', description: 'Platform for testing')               
    }
    
    notify('Started')
    try {
        stage('checkout') {
        git 'https://github.com/annajel/helloworld.git'
        }
        
        stage('compile, test, package, deploy') {
            withMaven(maven: 'maven'){
            sh label: '', script: 'mvn clean package jelastic:deploy'
            }
        }
        
        stage('archival') {
            archiveArtifacts 'target/*.war'
        }
        
        notify('Success')
        
    } catch (err) {
        notify("Error ${err}")
        echo "Caught: ${err}"
        currentBuild.result = 'FAILURE'
    }
}

def notify(status){
    emailext (
      from: "jenkins@cluster.com",
      to: "ash@mailhog.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}


