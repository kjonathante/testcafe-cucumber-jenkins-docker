node {
  stage('First') {
    checkout scm
    def browsers = docker.build('browsers:latest','docker/browsers/')
    browsers.inside {
      sh 'touch index.html'
      sh 'ls -la > results.txt'
    }
  }
}
