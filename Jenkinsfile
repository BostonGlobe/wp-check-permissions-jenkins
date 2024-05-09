/**
* Pipeline enabling the recreation of the HTML sitemap for the current month.
*
* - Clear cache if it exists to ensure retrieval of the latest values.
* - Trigger the bdc-html-sitemap create command to generate the HTML sitemap for the current month.
* - Assign appropriate permissions to the generated file for browser visualization.
*/

pipeline {
    agent { label 'wordpress' }
    parameters {
        string(
            name: 'wordpressPath',
            description: 'WordPress installation path.'
        )
        booleanParam(
            name: 'skipCacheCleaning',
            defaultValue: false,
            description: 'Skip the stage of cache clearing.'
        )
        string(
            name: 'staticSitemapsDir',
            defaultValue: '../content/uploads/bdc-static-sitemaps/',
            description: 'Static sitemaps directory.'
        )
    }
    environment {
        YEAR = sh(script: 'date "+%Y"', returnStdout: true).trim()
        MONTH_NUMBER = sh(script: 'date "+%m"', returnStdout: true).trim()
    }
    stages {
        stage('chown') {
            steps {
                script {
                    // This command recreates the HTML sitemap exclusively for the current month.
                    //sh "dzdo -u root wp bdc-html-sitemap create --path='${wordpressPath}' --allow-root"
                    // Assigning permissions 0644 grants read and write access to the file owner, and read-only access to group and other users.
                    sh "dzdo chown -R nobody2:nobody /sandbox/blogs/bgsponsored__word-3458-v2/uploads"
                    sh "dzdo chown -R nobody2:nobody /sandbox/blogs/bgsponsored__word-3458-v2/content/uploads"
                    //dzdo -u root chmod 644 '${wordpressPath}${params.staticSitemapsDir}${env.YEAR}-${env.MONTH_NUMBER}.html'"
                }
            }
        }
    }
}
