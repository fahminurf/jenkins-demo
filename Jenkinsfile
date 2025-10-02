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
		sh '. venv/bin/activate && pytest -v'
		sh 'echo "Test Selesai"'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Stage Deploy  : Simpan Hasil ke Workspace "'
		sh 'mkdir -p deploy-demo'
		sh 'cp script.sh deploy-demo/'
		sh 'tar -czf deploy-demo-$(date +%Y%m%d-%H%M%S).tar.gz deploy-demo/'
            }
        }
    }

   post {
	success{
		archiveArtifacts artifacts: 'deploy-demo-*.tar.gz', fingerprint: true
		sh 'echo "berhasil, berhasil hore, hore"'
	}
	failure{
		sh 'echo "gagal maning sonnnn, cek log"'
	}
   }
}
