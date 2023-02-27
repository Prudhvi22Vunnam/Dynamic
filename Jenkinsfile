pipeline {
    agent any

    parameters {
        file(name: 'FILE_TO_COPY', description: 'File to be copied to EFS')
        string(name: 'EFS_MOUNT_POINT', description: 'Mount point of the EFS filesystem')
        string(name: 'EFS_DIRECTORY', description: 'Directory path in EFS to copy the file to')
    }

    stages {
        stage ('identify the file')
            steps {
              sh "cd /directory"
              
        stage('Copy file to EFS') {
            steps {
                script {
                    sh "aws efs create-directory --region <REGION> --file-system-id <FILE_SYSTEM_ID> --parent-directory <EFS_DIRECTORY>"
                    sh "aws efs describe-file-systems --region <REGION> --file-system-id <FILE_SYSTEM_ID>"
                    sshCommand remoteUser: <REMOTE_USER>, remotePassword: <REMOTE_PASSWORD>, remoteHost: <REMOTE_SERVER>, command: "sudo mount -t nfs4 <FILE_SYSTEM_ID>.efs.<REGION>.amazonaws.com:/ <EFS_MOUNT_POINT>"
                    sshCommand remoteUser: <REMOTE_USER>, remotePassword: <REMOTE_PASSWORD>, remoteHost: <REMOTE_SERVER>, command: "sudo cp ${params.FILE_TO_COPY} ${params.EFS_MOUNT_POINT}/${params.EFS_DIRECTORY}"
                    sshCommand remoteUser: <REMOTE_USER>, remotePassword: <REMOTE_PASSWORD>, remoteHost: <REMOTE_SERVER>, command: "sudo umount ${params.EFS_MOUNT_POINT}"
                }
            }
        }
    }
}
