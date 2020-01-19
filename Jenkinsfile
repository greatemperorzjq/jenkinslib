#!groovy

@Library('jenkinslib') _

def tools = new org.devops.tools()  //定义的lib中org文件下的devops下的tools文件


String workspace = "/opt/jenkins/workspace"

pipeline {
   agent { node {label "build"
                customWorkspace "${workspace}"
         }
    }
         
   options {
       timestamps() //日志显示时间
       skipDefaultCheckout()  //删除隐式checkout scm语句
       disableConcurrentBuilds() //禁止并行
       timeout(time: 1, unit: 'HOURS') //流水线超时设置1小时
   }
   
  
   stages {
     //下载代码
      stage('GetCode') {
         steps {
             timeout(time: 5, unit: "MINUTES"){
                 script{
                     print('获取代码')
                    
                     tools.PrintMes("获取代码","green")
                }
         }
      }
}   
   
     //构建
      stage('Build') {
         steps {
             timeout(time: 20, unit: "MINUTES"){
                 script{
                     print('应用打包')
                    
                     tools.PrintMes("应用打包","green")
                }
         }
      }
   }
  
  //代码扫描
      stage('CodeScan') {
         steps {
             timeout(time: 30, unit: "MINUTES"){
                 script{
                     print('代码扫描')
                     
                     tools.PrintMes("代码扫描","green")
                }
         }
      }
  }
}

  //构建后操作
     post {
        always{
            script{
                println("always")
            }
        }
        
        success{
            script{
                currentBuild.description += "\n 构建成功!"
            }
        }
        
        failure{
            script{
                currentBuild.description += "\n 构建失败!"
            }
        }
        
        aborted{
            script{
                currentBuild.description += "\n 构建取消!"
            }
        
        }
    
    }
}
