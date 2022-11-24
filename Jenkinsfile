pipeline {
    agent none

    triggers {
        URLTrigger(
            cronTabSpec: '* * * * *',
            triggerLabel: 'windows',
            entries: [
                URLTriggerEntry( 
                    url: 'https://api.github.com/repos/jiabh/test-jenkins-url-trigger/releases/latest',
                    requestHeaders: [
                        RequestHeader( headerName: "Accept" , headerValue: "application/json" )
                    ],
                    contentTypes: [
                        JsonContent(
                            [
                                JsonContentEntry(jsonPath: '$.assets[?(@.name =~ /test-v.*?\\.txt/)].name')
                            ])
                    ]
                )
            ]
        )
    }

    stages {
        stage('Print hello world') {
            agent {
                docker { image 'node:18.12.1-alpine' }
            }
            steps {
                sh('node main.js')
            }
        }
    }
}
