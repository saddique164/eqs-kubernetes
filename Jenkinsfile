
pipeline {

    agent {node { label "server1" }}

    environment {

     git_repo = "git@github.com:saddique164/eqs-kubernetes-eqs.git"
     node_name = "master"
     playbook_path = "/jenkins-home/workspace/eqs-kubernetes-pipeline/roles/playbook.yaml"
	// nginx_deployment = "/jenkins-home/workspace/eqs-kubernetes-pipeline/roles/nginx.yaml"
        }

            stages {

                        stage ('git repository clone') {

                          steps {
                          git branch: "${env.node_name}", url:  "${env.git_repo}"
                            }
                        }

                        stage ('run ansible playbook'){

                                steps {
                                sh label: '', script: 'python --version'
                                ansiblePlaybook inventory: '/etc/ansible/hosts', playbook: "${env.playbook_path}"
                                 }
                        }
			stage ('deploy nginx pod in the cluster'){
                               agent {node { label "Kubernetes-cluster" }}
                                steps {
                                 sh label: '', script: 'scp /ansible/roles/nginx.yaml ubuntu@54.213.167.104:/nginx/'
                                 sh label: '', script: 'echo Saddique'


                                 }
                        }
						
            }
  }

