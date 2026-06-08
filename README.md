# Goodbaby 培训签到系统

基于 Supabase 数据库的培训签到系统，支持扫码签到/签退、二维码生成、数据导出等功能。

## 功能特点

- 培训信息管理（课程、日期、时间、讲师等）
- 扫码签到/签退（微信扫描二维码填写信息）
- 实时数据同步（多设备同时使用）
- 参会人员名单展示（25行两排，共50人）
- 历史记录管理（查看/加载/删除历史培训）
- Excel 导出
- 打印样式优化

## 部署到 Vercel

### 方法一：命令行部署

1. 安装 Vercel CLI：
```bash
npm i -g vercel
```

2. 登录：
```bash
vercel login
```

3. 进入项目目录并部署：
```bash
cd public
vercel --prod
```

4. 部署成功后获得固定地址，如：`https://your-project.vercel.app`

### 方法二：GitHub 部署（推荐）

1. 将整个项目推送到 GitHub 仓库
2. 访问 [vercel.com](https://vercel.com)
3. 点击 "New Project"，导入 GitHub 仓库
4. Vercel 会自动检测为 Static Site
5. 点击 Deploy，获得固定地址

## 以后更新代码

修改 `public/index.html` 后：

**命令行**：
```bash
cd public
vercel --prod
```

**GitHub**：
```bash
git add .
git commit -m "更新代码"
git push
```
Vercel 会自动重新部署，地址不变。

## 目录结构

```
project/
├── public/
│   └── index.html    # 主页面（所有代码）
├── README.md         # 部署说明
└── 公网地址.txt      # 记录固定访问地址
```

## 技术栈

- 前端：HTML/CSS/JavaScript（单文件）
- 数据库：Supabase (PostgreSQL)
- 二维码：QRCode.js
- Excel 导出：SheetJS
- 部署：Vercel

## 数据库表结构

### training_info（培训信息表）
| 字段 | 类型 | 说明 |
|------|------|------|
| id | uuid | 主键 |
| course | text | 培训课程 |
| train_date | date | 培训日期 |
| train_time | text | 培训时间 |
| total_hours | numeric | 总培训小时 |
| trainer | text | 培训师 |
| total_count | integer | 总培训人数 |
| location | text | 培训地点 |
| organizer | text | 组织者 |
| created_at | timestamp | 创建时间 |

### sign_records（签到记录表）
| 字段 | 类型 | 说明 |
|------|------|------|
| id | uuid | 主键 |
| training_id | uuid | 关联培训ID |
| row_index | integer | 行序号(0-49) |
| department | text | 部门 |
| emp_id | text | 员工编号 |
| name | text | 姓名 |
| signature | text | 签名（签退时填入） |
| sign_type | text | 签到类型 |
| created_at | timestamp | 创建时间 |
