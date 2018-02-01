
node {
    stage('Checkout') {
        checkout scm
    }
    stage('Build') {
        withMaven(maven: 'Maven 3.x') {
            // Run the maven build
            sh "mvn clean package"
        }
    }
}

node {
    stage('DepStop, Deploy and Start') {
        // Stop
        sh 'curl -X POST http://localhost:8080/shutdown || true'

        // Deploy
        sh 'cp target/*.jar /tmp/'
        sh 'nohup java -jar /tmp/*.jar &'

        // Start and wait for startup
        sh 'while ! httping -qc1 http://localhost:8080 ; do sleep 1 ; done'
    }
}

