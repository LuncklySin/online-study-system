# 🎓 在线学习系统 -- 更多在微信 ： jackSinWu --在咸鱼：不知名选手java小鑫 --B站：不知名选手java小鑫 关注可打9折

**在线学习系统** 是一个面向学生和自学者打造的在线教育平台，支持课程购买、免费学习、笔记记录、章节视频学习等功能，致力于提供高效、个性化的学习体验。平台引入沙箱支付测试机制，结合暴力打点算法保障视频完整观看记录，提升课程完成率与教学质量。

![image](https://github.com/user-attachments/assets/ef4bff20-12bb-4372-8b74-ea932a5a7ae5)
![image](https://github.com/user-attachments/assets/289dcd88-384e-4c62-9816-4651482f4c11)
![image](https://github.com/user-attachments/assets/77dda48c-9739-4ee9-aa18-7027f47b0b9c)
![image](https://github.com/user-attachments/assets/b5fc5aea-8130-4a5d-9b5e-20035945616a)
![image](https://github.com/user-attachments/assets/823bc70f-c7c8-4a66-bbed-3d723a93992f)
![image](https://github.com/user-attachments/assets/fd2c2fb0-2793-42b0-a728-257c1955215c)
![image](https://github.com/user-attachments/assets/ed1a0381-5d35-4754-9579-3b9e0084896e)


## 🛠 技术栈

- **前端**：Vue.js + Vuex + ElementUI
- **后端**：Spring Boot + MyBatis + Shiro + WebSocket  
- **数据库**：MySQL  
- **视频存储**：MinIO 
- **支付系统**：沙箱环境接入支付宝

---

## 🌟 核心功能模块

### 1. 用户管理模块

- 用户注册与登录（手机号 / 邮箱）  
- 用户认证与权限控制（学生 / 老师 / 管理员）  
- 用户信息修改与学习记录查看  
- 消息通知（课程公告、支付成功、学习提醒）

---

### 2. 课程管理模块

- 课程列表（免费课程 / 付费课程）  
- 课程详情页（封面、简介、讲师介绍、章节目录）  
- 支持课程分类、搜索、标签筛选  
- 老师后台上传课程、设置免费或付费状态  
- 课程价格配置，支持促销价 / 原价

---

### 3. 课程购买与支付模块

- 加入课程购物车 / 立即购买  
- 订单生成与状态跟踪  
- 沙箱支付对接（支付宝沙箱 / 微信沙箱环境）  
- 支付结果异步通知与回调处理  
- 购买记录管理（可查询历史订单、下载发票）

---

### 4. 视频学习模块

- 支持按章节观看视频课程  
- 视频播放器防快进机制（暴力打点算法）  
- 视频打点机制：每 N 秒记录播放位置，防止拖拽跳过  
- 视频观看进度保存与断点续播  
- 学习进度统计（学习率、视频完成率）

---

### 5. 学习笔记模块

- 学习中随时记录笔记  
- 每条笔记可关联章节与时间点  
- 富文本笔记支持插入代码块、图片、引用  
- 笔记导出为 PDF / Markdown  
- 收藏笔记 / 分享笔记（公开分享到学习社区）

---

### 6. 后台管理模块

- 课程审核与发布  
- 用户管理（权限分配、用户封禁）  
- 订单与支付记录查看  
- 内容管理（笔记审核、评论管理）  
- 数据可视化（学习时长、活跃用户、课程销售统计）

---

## 💡 技术难点与解决方案

### ✅ 视频防快进打点算法（暴力打点）

> **难点**：防止用户通过拖拽进度条跳过学习视频，从而绕过学习任务。

**解决思路**：

1. **打点记录**：每 5 秒记录一次播放进度（时间戳 + 课程章节 ID）。
2. **区间验证**：只有连续播放区间 > 90% 才算完成该视频。
3. **前端限制拖拽**：播放器配置 `seeked` 事件强制跳回上一个播放点。
4. **后端校验**：学习完成状态需后端比对打点完整性。

---

### ✅ 沙箱支付接入（支付宝 / 微信）

> **难点**：在不产生真实支付的前提下测试支付流程。

**解决方案**：

- 接入支付宝沙箱环境，获取测试商户号与公钥  
- 配置支付异步回调接口验证订单状态  
- 后台设置测试订单与用户积分发放逻辑  
- 支持支付失败 / 超时 / 成功的状态回调处理

---

## 🚀 项目部署指南

### ✅ 环境要求

| 环境 | 要求 |
|------|------|
| JDK | 11+ |
| Node.js | 16+ |
| MySQL | 8+ |
| MinIO | 任意版本 |
| 支付沙箱 | 支持支付宝沙箱或微信沙箱 |

---

### ▶ 后端部署

```bash
cd backend
mvn clean package
java -jar target/learning-system.jar
```

---

### ▶ 前端部署

```bash
cd frontend
npm install
npm run serve
```

---

### ▶ MinIO 配置

```bash
minio server /data --console-address ":9001"
```

配置示例 `application.yml`：

```yaml
minio:
  endpoint: http://localhost:9000
  accessKey: your-access-key
  secretKey: your-secret-key
  bucketName: course-videos
```

---

## 📁 项目结构

```
online-learning-system/
├── backend/         # Spring Boot 后端
│   ├── src/
│   └── pom.xml
├── frontend/        # Vue 或 UniApp 前端
│   ├── src/
│   └── package.json
├── docs/            # 文档
├── README.md
```

---

## 📊 数据统计示例

- 用户总数 / 注册增长图表  
- 各课程观看进度热力图  
- 用户日均学习时长趋势图  
- 订单销售总额 / 月度对比

---

## 📌 TODO（可拓展功能）

- 💬 课程评论与问答互动区  
- 📝 课程测验与考试模块  
- 📱 移动端推送提醒（签到 / 学习未完成）  
- 📹 视频直播课程（集成直播 SDK）  
- 📚 讲师分成与结算模块

---

## 📬 联系与贡献

欢迎提交 Issue、Fork 本项目或参与贡献：

- 📧 Email: example@example.com  
- ⭐ GitHub: 欢迎 Star 支持项目成长！

---

## 📄 License

本项目使用 MIT 协议，详情查看 [LICENSE](./LICENSE) 文件。
