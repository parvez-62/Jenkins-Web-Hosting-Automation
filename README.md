# Jenkins Web Hosting Automation

This project demonstrates how to set up automated web hosting using Jenkins CI/CD pipeline. The project uses Jenkins to automatically deploy web content from a GitHub repository to a web server.

## Prerequisites

- Ubuntu Server (tested on Ubuntu with IP 13.234.78.5)
- Jenkins 2.485
- Java OpenJDK 17.0.13
- Git 2.43.0
- GitHub account

## System Requirements

- OpenJDK Runtime Environment (build 17.0.13+11-Ubuntu-2ubuntu124.04)
- OpenJDK 64-Bit Server VM (mixed mode, sharing)
- Minimum 96.9 MB of disk space for Jenkins installation

## Installation Steps

### 1. Install Java

```bash
sudo apt update
java --version  # Verify Java installation
```

### 2. Install Jenkins

```bash
# Add Jenkins repository
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/sources.list.d/jenkins.list'

# Install Jenkins
sudo apt update
sudo apt install jenkins
```

### 3. Configure Jenkins

1. Access Jenkins at `http://your-server-ip:8080`
2. Install suggested plugins including:
   - Folders
   - Pipeline
   - Git
   - GitHub Branch Source
   - SSH Build Agents

## Project Setup

1. Create a new Pipeline project in Jenkins
2. Configure GitHub repository connection
3. Configure build triggers
4. Set up workspace at `/var/lib/jenkins/workspace/my-project123`

## Pipeline Configuration

```groovy
pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/your-username/your-repo.git'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'cp -r * /var/www/html/'
            }
        }
    }
}
```

## Project Structure

```
my-project123/
├── index.html
└── styles/
    └── main.css
```

## Features

- Automated deployment from GitHub to web server
- Real-time console output for build monitoring
- Support for HTML, CSS, and JavaScript content
- Automatic git fetch and checkout

## Security Notes

- Jenkins runs as SYSTEM user
- Proper credentials configuration required for GitHub integration
- HTTPS recommended for production deployment

## Troubleshooting

Common issues and solutions:
1. If build fails with git errors, verify:
   - Git installation
   - Repository permissions
   - Credentials configuration
2. For deployment issues:
   - Check web server permissions
   - Verify workspace path
   - Review console output for specific errors

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.
