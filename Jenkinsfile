pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "Stage Build "'
                sh 'chmod +x script.sh'
                sh './script.sh'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Stage Test : coba menjalankan pytest"'
		sh 'python3 -m venv venv'
		sh '. venv/bin/activate && pip install -r requirements.txt'
		sh '. venv/bin/activate && pytest -v --html=report.html --self-contained-html || true'
		sh 'echo "Test Selesai"'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Stage Deploy  : Simpan Hasil ke Workspace "'
		sh 'mkdir -p deploy-demo'
		sh 'cp script.sh deploy-demo/'
		sh 'tar -czf deploy-demo-${BUILD_NUMBER}.tar.gz deploy-demo/'
            }
        }
    }

   post {
	always {
		archiveArtifacts artifacts: 'report.html', fingerprint:true
	}
	success{
		archiveArtifacts artifacts: 'deploy-demo-${BUILD_NUMBER}.tar.gz', fingerprint: true
		sh 'echo "berhasil, berhasil hore, hore"'
	}
	failure{
		sh 'echo "gagal maning sonnnn, cek log"'
	}
   }
}
