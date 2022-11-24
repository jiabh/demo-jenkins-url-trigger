pipeline {
    agent any

    triggers {
        URLTrigger(
            cronTabSpec: '* * * * *',
            triggerLabel: 'windows',
            entries: [
                URLTriggerEntry( 
                    url: 'https://api.github.com/repos/jiabh/test-jenkins-url-trigger/releases/latest',
                    contentTypes: [
                        TextContent(
                            [
                                TextContentEntry(regEx: 'test-v.*?.txt')
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
