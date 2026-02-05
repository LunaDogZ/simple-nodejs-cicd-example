pipeline {
  environment {
    VERCEL_PROJECT_NAME = 'DevOp16_simple-nodejs' 
    VERCEL_TOKEN = credentials('DevOp16-simple-nodejs') 
  }
  
  agent {
    docker {
      image 'node:20-alpine'
      args '-u root' 
    }
  }

  stages {
    stage('Install Dependencies') {
      steps {
        sh 'npm ci' 
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