@Library('shared') _
pipeline {
    agent any
    
    parameters {
        string(name: 'IMAGE_TAG', defaultValue: '', description: 'Docker image tag to deploy')
    }
    
    environment{
        GIT_REPO_URL = "https://github.com/Saim0704/Wanderlust-Manifest.git"
        GIT_BRANCH = "main"
        GITHUB_CRED = "Github"
        DOCKER_REPO_NAME = "wanderlust-frontend"
        
    }
    stages {
        stage('Code Clone') {
            steps {
                git_checkout("${env.GIT_REPO_URL}", "${env.GIT_BRANCH}")
            }
        }
        stage('Update Manifest'){
            steps{
                echo "Update Manifest"
                update_manifest("${env.DOCKER_REPO_NAME}", "${params.IMAGE_TAG}")
            }
        }
        stage('Push Updates to GitHub'){
            steps{
                echo "Push Updates to GitHub"
                push_to_github("${env.GIT_REPO_URL}", "${env.GIT_BRANCH}", "${env.GITHUB_CRED}")
            }
        }
    }
    post {
        always {
            cleanWs()
            // script {
            //     sh "echo 'y' | docker system prune -a"
            // }
        }
    }
}
