pipeline {
    agent any
    environment { 
        LOG='/var/log/apache2/access.log'
        REPORT='apache_log_report.txt'
    }

    stages {
        stage('Check logs & archive') {
            steps {
                sh '''
                    echo "Apache log report: $(date)" > $REPORT
                    if [ -f "$LOG" ]; then
                        echo "\\n=== 4xx ===" >> $REPORT
                        grep -E '" 4[0-9]{2} ' $LOG >> $REPORT || echo "No 4xx" >> $REPORT
                        echo "\\n=== 5xx ===" >> $REPORT
                        grep -E '" 5[0-9]{2} ' $LOG >> $REPORT || echo "No 5xx" >> $REPORT
                    else
                        echo "Log not found: $LOG" >> $REPORT
                    fi
                '''
                archiveArtifacts artifacts: REPORT, fingerprint: true
            }
        }
    }

    post {
        always { echo 'Pipeline finished.' }
    }
}
