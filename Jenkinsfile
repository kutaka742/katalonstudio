#!/usr/bin/env groovy

pipeline {

    //���s�m�[�h��ݒ�
    agent{
        label 'master'
    }

    //����W���u�̕��s���s�s��(���s���s�\�Ƃ���Ȃ�option���ƍ폜)
    options{
        disableConcurrentBuilds()
    }

    stages {
        //���[�N�X�y�[�X�N���A
        stage('Clear') {
            steps {
                script{
                    cleanWs()
                }
            }
        }

        //�`�F�b�N�A�E�g
        stage('Checkout') {
            steps {
                script{
                    checkout scm
                }
            }
        }

        //Katalon�e�X�g
        stage('Test') {
            steps {
                script{
                    try {
                        bat "C:\\KatalonStudio\\katalon -noSplash -runMode=console -projectPath=\"${env.WORKSPACE}\\project\\GoogleSerch.prj\" -retry=0 -testSuitePath=\"Test Suites/CheckOKTest\" -executionProfile=\"default\" -browserType=\"IE\""
                    } catch (Exception e) {
                        echo "�e�X�g���s�G���["
                    } finally {
                        //�e�X�g���ʕۑ�
                        archiveArtifacts artifacts: '**/Reports/**/*.*'
                    }
                }
            }
        }
    }
    post{
        always{
            //���[�N�X�y�[�X�N���A
            cleanWs()
        }
        failure{
            echo "�G���["
        }
        success{
            echo "����"
        }
        unstable{
            echo "�s����"
        }
    }
}
