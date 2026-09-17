# 身知回响复现说明

本说明以“GOAI赛道2项目沉淀包”的真实目录为准。源码位于：

```text
../03-完整代码/身知回响-可复现源码-V1.0.zip
```

复现分为两层：

- **本地核心流程**：Web Demo无需小程序账号、CloudBase或模型Key；
- **微信云端能力**：需要自备小程序AppID、关联腾讯云账号、CloudBase环境和模型API Key。

## 1. 解压源码

将源码ZIP解压到独立目录，然后进入包含 `package.json`、`src/`、`miniprogram/` 和 `cloudfunctions/` 的源码根目录。后续命令都在该目录执行。

## 2. 复现Web Demo

环境：

- Node.js 20或以上；
- npm；
- 现代浏览器。

运行：

```bash
npm install
npm run dev
```

访问：

```text
http://localhost:3000/agent
```

Web Demo不调用在线模型，不需要API Key。完成提问、挑战、费曼解释和节点点亮，即可验证核心学习闭环。

## 3. 运行质量检查

```bash
npm test
npm run lint
npm run typecheck
npm run typecheck:mini
npm run build
```

公开源码发布前已通过19个测试文件、64项测试、Lint、Web与小程序类型检查和生产构建。

## 4. 导入微信小程序

1. 注册微信小程序并取得自己的AppID；
2. 安装微信开发者工具；
3. 选择“导入项目”；
4. 项目目录选择解压后的**源码根目录**，不要只选择 `miniprogram/`；
5. 将 `project.config.json` 中的占位AppID替换为自己的AppID；
6. 点击“编译”。

公开占位AppID不能保证在所有开发者工具版本中使用。出现“不存在此AppID”或错误码10时，必须换成自己注册的AppID或测试号。

## 5. 启用云端能力

完整云端能力需要：

- 小程序AppID；
- 与小程序正确关联的腾讯云账号；
- CloudBase环境；
- 四个已部署云函数；
- 可选模型API Key。

请严格按照[部署说明](./部署说明.md)操作。只替换AppID和环境ID不足以建立权限，必须完成小程序、腾讯云账号和CloudBase环境关联。

## 6. Demo验收路径

1. 打开能力地图；
2. 进入“感知与传感器”；
3. 阅读传感器选择微课；
4. 完成仓储AMR挑战；
5. 提交一次费曼复述；
6. 按证据反馈补充答案；
7. 重新提交并点亮节点；
8. 进入案例页完成知识迁移。

演示脚本：[Demo演示脚本](../05-Demo/Demo演示脚本.md)。

无法现场运行时，可使用同目录的 `Demo演示视频.mp4`。

## 7. 常见问题

模型Key、AppID、CloudBase、知识库替换、模拟器白屏和复现标准见[项目复现FAQ](../06-FAQ/项目复现FAQ.md)。

## 8. 复现成功标准

- Web `/agent` 页面能够打开；
- 本地提问能返回课程依据；
- 挑战和费曼复述能提交；
- 确定性规则能判断是否点亮；
- 刷新后本地进度仍能恢复；
- 启用云端后，`healthCheck` 调用成功；
- 云端不可用时，学习主流程诚实降级而不中断。
