
pipeline {
  agent any
  parameters {
    string(name: 'BRANCH', defaultValue: 'master', description: 'git branch name')
    string(name: 'NODE', defaultValue: '172.31.19.119', description: 'web server node')
  }
  stages {
    stage('build') {
      steps {
        echo 'building...'
	git branch: "${params.BRANCH}", url: 'https://github.com/patilmahadev/jenkins-test.git'
	sh 'sudo cp -f index.html /var/lib/jenkins/cookbooks/apache/files/'
	sh 'sudo knife cookbook upload apache --force'
      }
    }
    stage('testing...') {
      steps {
        sh 'date'
        echo 'test cases ran successfully!'
      }
    }
    stage('deploy') {
      steps {
        echo 'deploying...'
	sh "sudo knife bootstrap ${params.NODE} --node-name websrv --ssh-user ec2-user --sudo --identity-file /root/chef-repo/.chef/wordpress.pem --run-list 'apache' -y"
      }
    }
  }
}
