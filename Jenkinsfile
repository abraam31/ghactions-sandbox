pipeline {
    agent any
    stages {
        stage('Test Step') {
            steps {
                script {
                    // Parse the GITURL to fetch the name of repo name
                    env.GIT_REPO_NAME = env.GIT_URL.replaceFirst(/^.*\/([^\/]+?).git$/, '$1')
                    // Read the hoover.yaml and put it in datas variable
                    datas = readYaml (file: 'hoover.yaml')
                    // Check if key exists in the created var
                    if(datas.containsKey("serviceName")){
                        env.service = datas.serviceName.toString()
                    }
                    /* 
                        If not assign the value of Repo name
                        Optional (commented): Rewrite the hoover.yaml
                    */
                    else {
                        env.service = "${GIT_REPO_NAME}"
                    /* Remove the comment if you want to rewrite the hoover.yaml
                        datas.service = "${service}"
                        sh "rm -rf hoover.yaml"
                        writeYaml file: "hoover.yaml", data: datas
                        sh "cat hoover.yaml"
                    */
                    }
                    echo "Service name is: ${service}"
                }
            }
        }
    }
}