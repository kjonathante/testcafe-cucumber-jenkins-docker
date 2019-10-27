node {
  stage('First') {
    checkout scm
    def browsersContainer = docker.build('browsers:latest','docker/browsers/')
    browsersContainer.inside {
      sh 'npm install'
      test('Chrome')
      sh 'npm run generateHtmlReport'
      sh 'ls -la > results.txt'
    }
  }
}

def test(BROWSER) {
  sh "npm run testDocker${BROWSER}"
}