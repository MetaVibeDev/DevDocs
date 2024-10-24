# Pushy热更方案使用手册

### Pushy热更方案整体流程
>一句话概括：还是按照之前的eas build + eas submit流程，只不过在eas build后将生成的包也传入pushy，作为原生包。后续热更包直接上传pushy就可实现热更。用户每次打开app或者从后台拉取app到前台时，app会向pushy服务器查询是否有新热更，如果有则提示用户下载。

#### 前期配置
1. 先全局安装命令行工具，每台电脑只用装一次
   `yarn global add react-native-update-cli`
2. （Mac专属）将 Yarn 全局路径添加到 .zshrc 文件中
   目的是为了确保系统可以找到 Yarn 全局安装的命令行工具。具体实现如下：
   - 找到Yarn全局路径：`yarn global bin` eg: /Users/scu/.yarn/bin
   - 打开 .zshrc 文件：`nano ~/.zshrc`
   - 在 nano 编辑器中，将以下行添加到文件的末尾：`export PATH="$PATH:$(yarn global bin)"` eg: export PATH="$PATH:/Users/scu/.yarn/bin"
   - 保存并退出
3. `yarn install`
4. `cd ios && pod install`
5. `pushy login`：登录pushy账号
   - 账号： 1554467581@qq.com
   - 密码： Zhusiyu1999

#### 打包+上传流程
1. `eas build` ----生成安卓和ios包（和之前无区别） eg: eas build --platform android --profile production
2. `eas submit` ----上传包到苹果开发者平台（和之前无区别） eg: eas submit --platform ios --profile production
3. 将安卓包和ios包下载到电脑本地，拿到本地包路径
4. `pushy uploadIpa/uploadApk <path_to_your_apk_file>`----上传包到pushy

#### 热更流程
1. `pushy bundle --platform android/ios`：上传热更包

### 参考
   pushy文档：https://pushy.reactnative.cn/docs/getting-started

### 注意事项


