node {
    def AppDir = '/var/www/nextjs-app'

    stage('Clean workspace') {
        deleteDir()
    }

    stage('Clone repo') {
        git branch: 'main', url: 'https://github.com/yashpatle741/Jenkins-CICD'
    }

    stage('Deploy to EC2') {
        sh """
          sudo mkdir -p ${AppDir}
          sudo chown -R jenkins:jenkins ${AppDir}

          rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${AppDir}

          cd ${AppDir}
          npm install
          npm run build

          sudo fuser -k 3000/tcp || true
          nohup npm run start > app.log 2>&1 &
        """
    }
}