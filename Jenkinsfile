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
        }
        success{
            echo "正常"
        }
        unstable{
            echo "不安定"
        }
    }
}
