pipeline {
  agent any
  stages {
    stage('Install browser firefox') {
      steps {
        bat '''
          npx playwright install firefox
        '''
        bat '''
          npm i -D @playwright/test allure-playwright
        '''
      }
    }  
    stage('test') {
      steps {
        bat '''
        npx playwright test --workers 6 --project=firefox --reporter=line,allure-playwright
        '''
      }
    }
  }
    post('allure report'){
      always{
        script {
          allure([
        includeProperties: false, 
        jdk: 'JDK', 
        results: [[path: 'allure-results']]
        ])
      }
    }
      failure{
        slackSend color: "bad", message: "https://russia-tv.online/che?region=77 I see an error in the console, maybe even CORS. CHECK!"
    }
  }
}