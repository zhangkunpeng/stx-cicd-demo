def label = "jenkins-jenkins-cicd"
podTemplate(label: label,cloud: "kubernetes" ){
    node(label) {
        stage('Clone') {
            echo "1.Clone Stage"
            git url: "https://github.com/zhangkunpeng/stx-cicd-demo.git"
            script {
                build_tag = sh(returnStdout: true, script: 'git rev-parse --short HEAD').trim()
            }
        }
        stage('Test') {
          echo "2.Test Stage"
        }
        stage('Build') {
          echo "3.Build Stage"
          sh "docker build -t registry.local:9001/stx-cicd-demo:latest ."
        }
        stage('Push') {
            echo "4.Push Docker Image Stage"
            sh "docker login -u admin -p 99cloud@SH registry.local:9001"
            sh "docker push registry.local:9001/stx-cicd-demo:latest"
        }
        stage('Deploy') {
          echo "5. Deploy Stage"
          sh "kubectl apply -f k8s.yaml"
        }
    }
}