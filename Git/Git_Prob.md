# Git的飞行规则

https://github.com/k88hudson/git-flight-rules/blob/master/README_zh-CN.md

## Git Problems
1. Failed to connect to github.com port 443:connection timed out
   ```shell
   # 取消全局代理：
   git config --global --unset http.proxy
   git config --global --unset https.proxy
   ```

2. 取消ssh验证

   ```shell
   git config --global http.sslVerify false
   ```

3. 配置http代理
    ```shell
    git config --global http.proxy 127.0.0.1:7890
    git config --global https.proxy 127.0.0.1:7890
    ```