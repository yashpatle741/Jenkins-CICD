node{
    def AppDir = '/var/www/nextjs-app'
    Stage('clean workspace'){
        echo 'cleaning jenkins workspace'
        deleteDir()
    }
    Stage('Clone repo'){
        echo 'cloning the repo'
        git(branch: 'main'
            url: 'https://github.com/yashpatle741/Jenkins-CICD.git'
            
            )
    }
    Stage('Deploy to EC2'){
        echo 'deploying to EC2'
        sh"""
          sudo mkdir -p ${AppDir}
          sudo chown -R Jenkins:Jenkins ${AppDir}

          rsync -av --delete --exclude = '.git' --exclude = 'node_modules' ./${AppDir}
          cd ${AppDir}
          sudo npm install
          sudo npm run build
          sudo fuser -k 3000/tcp || true
          npm run start
          """
    }
}