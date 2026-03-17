node{
    def appDir= '/var/www/nextjs-app'
    stage('Clean Workspace'){
        echo "Cleaning Working Directory"
        deleteDir()
    }
    stage('clone repo'){
        echo "cloning repo"
        git(
            branch:'main',
            url:'https://github.com/AbulAlaJobayar/-CI-CD-Pipeline-with-Jenkins-GitHub-Webhook-AWS-EC2-for-Next.js-Deployment'
        )
    }
    stage('deploy to server'){
        echo "deploying to server"
        sh """
        sudo mkdir -p ${appDir}
        sudo chown -R jenkins:jenkins ${appDir}
        rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}/
        cd ${appDir}
        npm install
        npm run build
        sudo fuser -k 3000/tcp || true
        nohup npm run start &
        """
    }
}