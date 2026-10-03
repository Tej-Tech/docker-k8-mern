pipeline {
  agent any

  environment {
    FRONTEND_IMAGE = "mern-frontend:jenkins"
    BACKEND_IMAGE  = "mern-backend:jenkins"
    PORT = "5000"
    MONGO_URI = "mongodb://mongo:27017/taskdb"
  }

  stages {
    stage('Checkout Code') {
      steps {
        git url: 'https://github.com/sangammukherjee/devops-youtube-course-2025.git', branch: 'dev'
      }
    }

    stage('Prepare .env') {
      steps {
        sh '''
          mkdir -p server
          cat > server/.env <<EOF
PORT=$PORT
MONGO_URI=$MONGO_URI
EOF
        '''
      }
    }

    stage('Run with Docker Compose') {
      steps {
        sh '''
          echo "Starting MERN stack with Docker Compose..."
          docker compose up --build -d

          echo "Showing running containers..."
          docker ps

          echo "===== Backend Logs ====="
          docker logs backend || true

          echo "===== Frontend Logs ====="
          docker logs frontend || true
        '''
      }
    }
  }
}
