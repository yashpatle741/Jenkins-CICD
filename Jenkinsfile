node{
    def AppDir = '/var/www/nextjs-app'
    stage('clean workspace'){
        echo 'cleaning jenkins workspace'
        deleteDir()
    }
    stage('Clone repo'){
        echo 'cloning the repo'
       git branch: 'main', url: 'https://github.com/yashpatle741/Jenkins-CICD'
    }
    stage('Deploy to EC2'){
        echo 'deploying to EC2'
        sh"""
          sudo mkdir -p ${AppDir}
          sudo chown -R jenkins:jenkins ${AppDir}

          rsync -av --delete --exclude= '.git' --exclude= 'node_modules' ./ ${AppDir}
          cd ${AppDir}
          sudo npm install
          sudo npm run build
          sudo fuser -k 3000/tcp || true
          npm run start
          """
    }
}