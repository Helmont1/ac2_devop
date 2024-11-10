pipeline {
  agent any
  stages {
    stage("verify tooling") {
      steps {
        bat '''
          docker version
          docker info
          docker compose version
          curl --version
          '''
      }
    }

    stage('Start container') {
      steps {
        bat docker-compose -f docker-compose.prod.yml up -d --no-color --wait'
        bat 'docker compose ps'
      }
    }
    stage('Run tests against the container') {
      steps {
        sleep time: 30, unit: 'SECONDS'
        bat 'curl http://localhost:8585'
      }
    }
  }

}