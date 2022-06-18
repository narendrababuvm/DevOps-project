node {
    
    stage('Pull Application code with GIT') {
        
        git branch: 'main', 
        credentialsId: 'sampleA-github-access', 
        url: 'git@github.com:narendrababuvm/DevOps-project.git'

    }
    stage('Building the web artifact') {
        // Run the maven build
        def mvnHome = tool 'MVN'
        withEnv(["MVN_HOME=$mvnHome"]) {
            
            sh '"$MVN_HOME/bin/mvn" clean compile package'
           
        }
    }
    stage('Deploy the Application war file on webservers') {
        // Run ansible
        ansiblePlaybook credentialsId: 'ansible-access', 
        installation: 'ANSIBLE', 
        inventory: '/var/lib/jenkins/workspace/sampleA-main/inventory', 
        playbook: '/var/lib/jenkins/workspace/sampleA-main/playbook.yml'
    }
}
