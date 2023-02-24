# Headline

## Git Problems
1. Failed to connect to github.com port 443:connection timed out
   ```shell
   # 取消全局代理：
   git config --global --unset http.proxy
   git config --global --unset https.proxy
   ```
2.  取消ssh验证

   ```shell
   git config --global http.sslVerify false
   ```

   