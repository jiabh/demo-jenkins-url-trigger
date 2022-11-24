pipeline {
    agent none

    triggers {
        URLTrigger(
            cronTabSpec: '* * * * *',
            /**
             * This param is not mentioned in the documentation of URLTrigger plugin,
             * but it's necessary when Jenkins build-in node is disabled.
             * See source code for more details:
             * https://github.com/jenkinsci/urltrigger-plugin/search?q=triggerLabel
             */
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
                                // Monitor "test-v0.0.1.txt" in release for example.
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
