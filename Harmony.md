## 资料信息

[开发文档](https://docs.openharmony.cn/pages/v4.0/zh-cn/application-dev/quick-start/start-overview.md)

[项目示例](https://gitee.com/openharmony/codelabs)

[Copy?](https://www.bilibili.com/video/BV1Dh4y1g7hR/?spm_id_from=333.976.0.0&vd_source=48967c9da100242a790cef3ee3c6d53c)

## 工具准备

1. 安装最新版[DevEco Studio](https://docs.openharmony.cn/pages/v4.0/zh-cn/release-notes/OpenHarmony-v4.0-release.md#配套关系)。
2. 请参考[配置开发环境](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/environment_config-0000001052902427-V3)，完成**DevEco Studio**的安装和开发环境配置。

完成上述操作及基本概念的理解后，可参照[构建第一个ArkTS应用（Stage模型）](https://docs.openharmony.cn/pages/v4.0/zh-cn/application-dev/quick-start/start-with-ets-stage.md)进行下一步体验和学习。

## ArkTS工程目录结构（Stage模型）

![project](https://docs.openharmony.cn/doc_v4.0_1717713913/zh-cn/application-dev/quick-start/figures/project.png)

- **AppScope > app.json5**：应用的全局配置信息。
- **entry**：OpenHarmony工程模块，编译构建生成一个HAP包。
  - **src > main > ets**：用于存放ArkTS源码。
  - **src > main > ets > entryability**：应用/服务的入口。
  - **src > main > ets > pages**：应用/服务包含的页面。
  - **src > main > resources**：用于存放应用/服务所用到的资源文件，如图形、多媒体、字符串、布局文件等。关于资源文件，详见[资源文件的分类](https://docs.openharmony.cn/pages/v4.0/zh-cn/application-dev/quick-start/resource-categories-and-access.md#资源分类)。
  - **src > main > module.json5**：模块配置文件。主要包含HAP包的配置信息、应用/服务在具体设备上的配置信息以及应用/服务的全局配置信息。具体的配置文件说明，详见[module.json5配置文件](https://docs.openharmony.cn/pages/v4.0/zh-cn/application-dev/quick-start/module-configuration-file.md)。
  - **build-profile.json5**：当前的模块信息 、编译信息配置项，包括buildOption、targets配置等。
  - **hvigorfile.ts**：模块级编译构建任务脚本，开发者可以自定义相关任务和代码实现。
  - **obfuscation-rules.txt**：混淆规则文件。混淆开启后，在使用Release模式进行编译时，会对代码进行编译、混淆及压缩处理，保护代码资产。
- **oh_modules**：用于存放三方库依赖信息。
- **build-profile.json5**：应用级配置信息，包括签名signingConfigs、产品配置products等。
- **hvigorfile.ts**：应用级编译构建任务脚本。

### 构建第一个页面

1. 使用文本组件。

   工程同步完成后，在“**Project**”窗口，点击“**entry > src > main > ets > pages**”，打开“**Index.ets**”文件，可以看到页面由Text组件组成。“**Index.ets**”文件的示例如下：

   ```
   // Index.ets
   @Entry
   @Component
   struct Index {
     @State message: string = 'Hello World';
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ts
   ```

2. 添加按钮。

   在默认页面基础上，我们添加一个Button组件，作为按钮响应用户点击，从而实现跳转到另一个页面。“**Index.ets**”文件的示例如下：

   ```
   // Index.ets
   @Entry
   @Component
   struct Index {
     @State message: string = 'Hello World';
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           // 添加按钮，以响应用户点击
           Button() {
             Text('Next')
               .fontSize(30)
               .fontWeight(FontWeight.Bold)
           }
           .type(ButtonType.Capsule)
           .margin({
             top: 20
           })
           .backgroundColor('#0D9FFB')
           .width('40%')
           .height('5%')
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ts
   ```

3. 在编辑窗口右上角的侧边工具栏，点击Previewer，打开预览器。第一个页面效果如下图所示：

   ![zh-cn_image_0000001311334976](https://docs.openharmony.cn/doc_v4.0_1717713913/zh-cn/application-dev/quick-start/figures/zh-cn_image_0000001311334976.png)

### 构建第二个页面

1. 创建第二个页面。

   - 新建第二个页面文件。在“**Project**”窗口，打开“**entry > src > main > ets**”，右键点击“**pages**”文件夹，选择“**New > ArkTS File**”，命名为“**Second**”，点击“**Finish**”。可以看到文件目录结构如下：

     ![secondPage](https://docs.openharmony.cn/doc_v4.0_1717713913/zh-cn/application-dev/quick-start/figures/secondPage.png)

     > **说明：**
     >
     > 开发者也可以在右键点击“**pages**”文件夹时，选择“**New > Page**”，则无需手动配置相关页面路由。

   - 配置第二个页面的路由。在“**Project**”窗口，打开“**entry > src > main > resources > base > profile**”，在main_pages.json文件中的“src”下配置第二个页面的路由“pages/Second”。示例如下：

     ```
     {
       "src": [
         "pages/Index",
         "pages/Second"
       ]
     }
     json
     ```

2. 添加文本及按钮。

   参照第一个页面，在第二个页面添加Text组件、Button组件等，并设置其样式。“**Second.ets**”文件的示例如下：

   ```
   // Second.ets
   @Entry
   @Component
   struct Second {
     @State message: string = 'Hi there';
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           Button() {
             Text('Back')
               .fontSize(25)
               .fontWeight(FontWeight.Bold)
           }
           .type(ButtonType.Capsule)
           .margin({
             top: 20
           })
           .backgroundColor('#0D9FFB')
           .width('40%')
           .height('5%')
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ts
   ```

### 实现页面间的跳转

页面间的导航可以通过[页面路由router](https://docs.openharmony.cn/pages/v4.0/zh-cn/application-dev/reference/apis/js-apis-router.md)来实现。页面路由router根据页面url找到目标页面，从而实现跳转。使用页面路由请导入router模块。

如果需要实现更好的转场动效等，推荐使用[Navigation](https://docs.openharmony.cn/pages/v4.0/zh-cn/application-dev/ui/arkts-navigation-navigation.md)。

1. 第一个页面跳转到第二个页面。

   在第一个页面中，跳转按钮绑定onClick事件，点击按钮时跳转到第二页。“**Index.ets**”文件的示例如下：

   ```
   // Index.ets
   // 导入页面路由模块
   import router from '@ohos.router';
   import { BusinessError } from '@ohos.base';
   
   @Entry
   @Component
   struct Index {
     @State message: string = 'Hello World';
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           // 添加按钮，以响应用户点击
           Button() {
             Text('Next')
               .fontSize(30)
               .fontWeight(FontWeight.Bold)
           }
           .type(ButtonType.Capsule)
           .margin({
             top: 20
           })
           .backgroundColor('#0D9FFB')
           .width('40%')
           .height('5%')
           // 跳转按钮绑定onClick事件，点击时跳转到第二页
           .onClick(() => {
             console.info(`Succeeded in clicking the 'Next' button.`)
            // 跳转到第二页
              router.pushUrl({ url: 'pages/Second' }).then(() => {
                console.info('Succeeded in jumping to the second page.')
              }).catch((err: BusinessError) => {
                console.error(`Failed to jump to the second page.Code is ${err.code}, message is ${err.message}`)
              })
           })
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ts
   ```

2. 第二个页面返回到第一个页面。

   在第二个页面中，返回按钮绑定onClick事件，点击按钮时返回到第一页。“**Second.ets**”文件的示例如下：

   ```
   // Second.ets
   // 导入页面路由模块
   import router from '@ohos.router';
   import { BusinessError } from '@ohos.base';
   
   @Entry
   @Component
   struct Second {
     @State message: string = 'Hi there';
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           Button() {
             Text('Back')
               .fontSize(25)
               .fontWeight(FontWeight.Bold)
           }
           .type(ButtonType.Capsule)
           .margin({
             top: 20
           })
           .backgroundColor('#0D9FFB')
           .width('40%')
           .height('5%')
           // 返回按钮绑定onClick事件，点击按钮时返回到第一页
           .onClick(() => {
             console.info(`Succeeded in clicking the 'Back' button.`)
             try {
               // 返回第一页
               router.back()
               console.info('Succeeded in returning to the first page.')
             } catch (err) {
                let code = (err as BusinessError).code;
                let message = (err as BusinessError).message;
               console.error(`Failed to return to the first page.Code is ${code}, message is ${message}`)
             }
           })
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ts
   ```

3. 打开Index.ets文件，点击预览器中的![zh-cn_image_0000001311015192](https://docs.openharmony.cn/doc_v4.0_1717713913/zh-cn/application-dev/quick-start/figures/zh-cn_image_0000001311015192.png)按钮进行刷新。效果如下图所示：

   ![zh-cn_image_0000001364254729](https://docs.openharmony.cn/doc_v4.0_1717713913/zh-cn/application-dev/quick-start/figures/zh-cn_image_0000001364254729.png)

### 使用真机运行应用

1. 将搭载OpenHarmony标准系统的开发板与电脑连接。

2. 点击**File** > **Project Structure…** > **Project** > **SigningConfigs**界面勾选“**Automatically generate signature**”，等待自动签名完成即可，点击“**OK**”。如下图所示：

   ![signConfig](https://docs.openharmony.cn/doc_v4.0_1717713913/zh-cn/application-dev/quick-start/figures/signConfig.png)

3. 在编辑窗口右上角的工具栏，点击![zh-cn_image_0000001364054485](https://docs.openharmony.cn/doc_v4.0_1717713913/zh-cn/application-dev/quick-start/figures/zh-cn_image_0000001364054485.png)按钮运行。效果如下图所示：

   ![zh-cn_image_0000001364254729](https://docs.openharmony.cn/doc_v4.0_1717713913/zh-cn/application-dev/quick-start/figures/zh-cn_image_0000001364254729.png)

恭喜您已经使用ArkTS语言开发（Stage模型）完成了第一个OpenHarmony应用，快来[探索更多的OpenHarmony功能](https://docs.openharmony.cn/pages/v4.0/zh-cn/application-dev/application-dev-guide.md)吧。