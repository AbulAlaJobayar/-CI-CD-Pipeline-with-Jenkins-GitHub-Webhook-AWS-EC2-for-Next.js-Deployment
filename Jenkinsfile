node{
    def appDir='var/www/nextjs-app'

    stage('clean workspace'){
        echo 'Cleaning workspace...'
        deleteDir()
    }
    stage('clone repository'){
        echo 'Cloning repository...'
        git(
            branch: 'main',
            url:'https://github.com/AbulAlaJobayar/-CI-CD-Pipeline-with-Jenkins-GitHub-Webhook-AWS-EC2-for-Next.js-Deployment'
        )
    }
    stage('deploy to ec2'){
        echo "Deploying to EC2 instance..."
        sh """
        sudo mkdir -p ${appDir}
        sudo chown -R
        jenkins:jenkins ${appDir}

        rsync -av --delete --exclude='.git --exclude='node_modules' ./ ${appDir}/
         cd ${appDir}
         sudo npm install
         sudo npm run build
         sudo fuser -k 3000/tcp ||true
         npm run start

        """
    }
}