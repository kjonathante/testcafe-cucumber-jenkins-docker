node {
  stage('Build Container') {
    checkout scm
    def browsersContainer = docker.build('browsers:latest','docker/browsers/')
    browsersContainer.inside {
      sh 'npm install'

      test('Chrome')

      publishReports()

    }
  }
}

def test(BROWSER) {
  sh "npm run testDocker${BROWSER}"
  stash name: "${BROWSER}-report-stash", includes: "**/reports/${BROWSER}.json"
}

def publishReports() {
  sh 'rm -rf reports'
  unstash 'Chrome-report-stash'
  sh 'npm run generateHtmlReport'
  Date date = new Date()
  String datePart = date.format('dd/MM/yyyy')
  String timePart = date.format('HH:mm:ss')
  GString dateTime = "_${datePart}_${timePart}"
  echo dateTime
}