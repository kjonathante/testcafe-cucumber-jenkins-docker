node {
  stage('First') {
    checkout scm
    def browsers = docker.build('browsers:latest','docker/browsers/')
    browsers.inside {
      sh 'npm install'
      sh 'npm run testDockerChrome'
      sh 'npm run generateHtmlReport'
      sh 'ls -la > results.txt'
    }
  }
}
