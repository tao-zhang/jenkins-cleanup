node() {
  timestamps {
    
    // Maven clean for each project, also delete archived artifacts  
    withMaven(mavenSettingsConfig: 'maven-settings-nexus') {  
        sh '''
        cd ../..
        for d in * .[a-zA-Z0-9]*; do
          echo "$d"
          if [ -d "$d/workspace" ] && [ -f "$d/workspace/pom.xml" ]]; then
            mvn clean -f "$d/workspace/pom.xml"
            find "$d" -type d -name archive -mtime +10 -prune -exec rm -rf {} +
          fi
        done
        '''
    }
    
    // Clean maven local repository of artifacts that are older than 90 days
    sh '''
    cd ~/.m2/repository/com/mycompany
    find . -type d -name 0.0.1-* -mtime +90  -prune -exec rm -rf {} +
    '''
  }
}
