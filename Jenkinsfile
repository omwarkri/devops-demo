pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/omwarkri/devops-demo.git', branch: 'main'
            }
        }

        stage('Deploy HTML to Nginx') {
            steps {
                sh '''
                    # Ensure Login.html exists
                    if [ ! -f Login.html ]; then
                        echo "ERROR: Login.html not found!"
                        exit 1
                    fi

                    # Clean old files from Nginx directory
                    sudo rm -rf /var/www/html/*

                    # Copy all project files (HTML, CSS, images)
                    sudo cp -r * /var/www/html/

                    # Rename Login.html to index.html for Nginx
                    if [ -f /var/www/html/Login.html ]; then
                        sudo mv /var/www/html/Login.html /var/www/html/index.html
                    fi

                    # Fix permissions to avoid 403 errors
                    sudo chown -R www-data:www-data /var/www/html
                    sudo chmod -R 755 /var/www/html

                    # Restart Nginx server
                    sudo systemctl restart nginx
                '''
            }
        }
    }
}
