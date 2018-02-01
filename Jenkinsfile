
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
        sh 'nohup java -Dserver.port=8090 -jar /tmp/sample*.jar &'

        // Start and wait for startup
        sh 'sleep 10'
        sh 'curl http://localhost:8090/hello'
    }
}

