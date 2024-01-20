pipeline {
  agent none
  stages {
    stage('Back-end') {
      agent {
        docker { image 'maven:3.8.1-adoptopenjdk-11' }
      }
      steps {
        sh '''
        cd hello-world-app
        mvn clean package
        mvn test
        java -cp target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.Hello
        '''
      }
    }
    stage('Front-end') {
      agent {
        docker { image 'node:16-alpine' }
      }
      steps {
        sh '''
        npm test
        npm install
        npm start &
        node hello.js
        '''
      }
    }
  }
}
