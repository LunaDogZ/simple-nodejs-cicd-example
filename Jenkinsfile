pipeline {
  agent any

  environment {
    VERCEL_PROJECT_NAME = 'DevOp16_SImple-Nodejs' 
    VERCEL_TOKEN = credentials('devop16-vercel-latest') 
  }
  
  stages {
    stage('Install Dependencies') {
      steps {
        sh 'npm install' 
      }
    }
    
    
    stage('Test') {
      steps {
        sh 'npm test' 
      }
    }

    stage('Deploy to Vercel') {
      steps {
        sh 'npm install -g vercel@latest'
        
        sh '''
          vercel pull --yes --environment=production --token=$VERCEL_TOKEN
          vercel build --prod --token=$VERCEL_TOKEN
          vercel deploy --prebuilt --prod --token=$VERCEL_TOKEN
        '''
      }
    }
  }
}