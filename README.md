# MyNest 项目

## 项目概述

MyNest 是一个基于 NestJS 框架开发的后端应用程序，提供用户认证、二维码登录和算法题库管理等功能。该项目采用了模块化的架构设计，使用 TypeORM 进行数据库操作，JWT 进行身份验证，并集成了 Swagger 用于 API 文档生成。

## 技术栈

- **框架**：NestJS 10.x
- **数据库**：MySQL (通过 TypeORM 连接)
- **认证**：JWT (JSON Web Token)
- **API 文档**：Swagger
- **其他工具**：QRCode 生成、加密工具等

## 功能模块

### 用户模块 (User Module)

用户模块负责处理用户注册、登录和身份验证相关功能。

- **注册功能**：支持用户通过手机号、昵称和密码进行注册
- **登录功能**：支持用户通过手机号和密码进行登录，登录成功后返回 JWT token
- **JWT 认证**：使用 JWT 策略进行用户身份验证

### 二维码模块 (QRCode Module)

二维码模块提供二维码生成和扫码登录相关功能。

- **二维码生成**：生成包含登录链接的二维码图片
- **二维码状态管理**：支持查询、更新二维码状态（未扫描、已扫描待确认、已确认、已取消、已过期）
- **扫码登录流程**：支持完整的扫码登录流程，包括扫描、确认和取消操作

### 算法模块 (Algorithm Module)

算法模块用于管理和提供算法题库相关功能。

- **题库列表**：获取算法题库中的所有题目
- **题目管理**：支持题目的增删改查操作

## 安装与运行

### 前置条件

- Node.js (v14 或更高版本)
- MySQL 数据库

### 安装步骤

1. 克隆项目到本地

```bash
git clone <项目仓库地址>
cd mynest
```

2. 安装依赖

```bash
npm install
# 或使用 pnpm
pnpm install
```

3. 配置数据库

在 `src/app.module.ts` 中修改数据库连接配置：

```typescript
TypeOrmModule.forRoot({
  type: 'mysql',
  host: '127.0.0.1',
  port: 3306,
  username: 'root',
  password: 'your_password',
  database: 'test',
  synchronize: true,
  autoLoadEntities: true,
})
```

4. 启动应用

```bash
# 开发模式
npm run start:dev

# 生产模式
npm run build
npm run start:prod
```

应用将在 http://localhost:3000 上运行。

## API 文档

启动应用后，可以通过访问 http://localhost:3000/api 查看 Swagger API 文档。

## 项目结构

```
src/
├── algorithm/         # 算法模块
│   ├── dto/           # 数据传输对象
│   ├── entities/      # 实体类
│   ├── question_bank/ # 题库文件
├── qrcode/            # 二维码模块
│   ├── dto/           # 数据传输对象
├── user/              # 用户模块
│   ├── dto/           # 数据传输对象
│   ├── entities/      # 实体类
├── utils/             # 工具函数
├── app.module.ts      # 应用主模块
├── main.ts            # 应用入口
```

## 功能演示

### 二维码登录流程

1. 客户端请求生成二维码：`GET /qrcode/generate`
2. 用户扫描二维码：`GET /qrcode/scan?id=xxx`
3. 用户确认或取消授权：`GET /qrcode/confirm?id=xxx` 或 `GET /qrcode/cancel?id=xxx`
4. 客户端轮询二维码状态：`GET /qrcode/check?id=xxx`

### 用户注册与登录

1. 用户注册：`POST /user/register`
2. 用户登录：`POST /user/login`

## 许可证

[MIT](LICENSE)