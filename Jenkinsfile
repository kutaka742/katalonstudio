#!/usr/bin/env groovy

pipeline {

    //実行ノードを設定
    agent{
        label 'master'
    }

    //同一ジョブの並行実行不可(並行実行可能とするならoptionごと削除)
    options{
        disableConcurrentBuilds()
    }

    stages {
        //ワークスペースクリア
        stage('Clear') {
            steps {
                script{
                    cleanWs()
                }
            }
        }

        //チェックアウト
        stage('Checkout') {
            steps {
                script{
                    checkout scm
                }
            }
        }

        //Katalonテスト
        stage('Test') {
            steps {
                script{
                    try {
                        bat "C:\\KatalonStudio\\katalon -noSplash -runMode=console -projectPath=\"${env.WORKSPACE}\\project\\GoogleSerch.prj\" -retry=0 -testSuitePath=\"Test Suites/CheckOKTest\" -executionProfile=\"default\" -browserType=\"IE\""
                    } catch (Exception e) {
                        echo "テスト実行エラー"
                    } finally {
                        //テスト結果保存
                        archiveArtifacts artifacts: '**/Reports/**/*.*'
                    }
                }
            }
        }
    }
    post{
        always{
            //ワークスペースクリア
            cleanWs()
        }
        failure{
            echo "エラー"
            //mail bcc: 'BCCメールアドレスを記載する', body: '通知内容を記載する', cc: 'CCメールアドレスを記載する', from: '', replyTo: '', subject: '件名を記載する', to: '宛先メールアドレスを記載する'
        }
        success{
            echo "正常"
            //mail bcc: 'BCCメールアドレスを記載する', body: '通知内容を記載する', cc: 'CCメールアドレスを記載する', from: '', replyTo: '', subject: '件名を記載する', to: '宛先メールアドレスを記載する'
        }
        unstable{
            echo "不安定"
            //mail bcc: 'BCCメールアドレスを記載する', body: '通知内容を記載する', cc: 'CCメールアドレスを記載する', from: '', replyTo: '', subject: '件名を記載する', to: '宛先メールアドレスを記載する'
        }
    }
}
