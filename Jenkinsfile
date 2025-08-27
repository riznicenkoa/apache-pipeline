  agent any
  environment { LOG=&apos;/var/log/apache2/access.log&apos;; REPORT=&apos;apache_log_report.txt&apos; }
  stages {
    stage(&apos;Check logs &amp; archive&apos;) {
      steps {
        sh &apos;&apos;&apos;
          echo &quot;Apache log report: $(date)&quot; &gt; $REPORT
          if [ -f &quot;$LOG&quot; ]; then
            echo &quot;\\n=== 4xx ===&quot; &gt;&gt; $REPORT
            grep -E &apos;&quot; 4[0-9]{2} &apos; $LOG &gt;&gt; $REPORT || echo &quot;No 4xx&quot; &gt;&gt; $REPORT
            echo &quot;\\n=== 5xx ===&quot; &gt;&gt; $REPORT
            grep -E &apos;&quot; 5[0-9]{2} &apos; $LOG &gt;&gt; $REPORT || echo &quot;No 5xx&quot; &gt;&gt; $REPORT
          else
            echo &quot;Log not found: $LOG&quot; &gt;&gt; $REPORT
          fi
        &apos;&apos;&apos;
        archiveArtifacts artifacts: REPORT, fingerprint: true
      }
    }
  }
  post { always { echo &apos;Done&apos; } }
}
