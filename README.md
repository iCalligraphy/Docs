# iCalligraphy - 智能书法学习平台

基于 Flask + SQLAlchemy + SQLite 的智能书法学习平台，前后端一体化部署。

## 功能特性

- 用户注册、登录（JWT 认证）
- 书法作品上传、浏览、搜索
- 作品点赞、收藏
- 评论、回复功能
- 个人主页、作品管理
- 社区交流
- 审核中心

## 技术栈

### 后端
- Flask 3.0.0（Web 框架）
- SQLAlchemy 2.0.23（ORM）
- SQLite（数据库）
- Flask-JWT-Extended（JWT 认证）
- Flask-CORS（跨域支持）

### 前端
- HTML5 + CSS3 + JavaScript
- 响应式设计

## 快速开始

### 一键启动（推荐）

#### Windows
双击运行 `start.bat`，或在命令行中：
```bash
start.bat
```

#### Linux/Mac
```bash
chmod +x start.sh
./start.sh
```

启动脚本会自动：
1. 检查并安装依赖
2. 初始化数据库（如果不存在）
3. 启动服务

启动成功后访问：**http://localhost:5000**

### 手动启动

#### 1. 安装依赖
```bash
cd Backend
pip install -r requirements.txt
```

#### 2. 配置环境变量（可选）
```bash
cp Backend/.env.example Backend/.env
# 编辑 .env 文件修改配置
```

#### 3. 初始化数据库
```bash
cd Backend
python init_db.py
```

这将创建测试账号：
- 管理员：`admin` / `admin123`
- 测试用户：`testuser` / `test123`

#### 4. 启动服务
```bash
cd Backend
python app.py
```

访问 **http://localhost:5000**

## 项目结构

```
iCalligraphy/
├── Backend/                # 后端代码
│   ├── app.py             # 主应用（集成前后端）
│   ├── config.py          # 配置文件
│   ├── models.py          # 数据库模型
│   ├── utils.py           # 工具函数
│   ├── init_db.py         # 数据库初始化
│   ├── requirements.txt   # Python 依赖
│   ├── routes/            # API 路由
│   │   ├── auth.py       # 认证
│   │   ├── works.py      # 作品
│   │   ├── users.py      # 用户
│   │   ├── comments.py   # 评论
│   │   └── collections.py # 收藏
│   └── uploads/          # 上传文件
├── Frontend-HTML/         # 前端代码
│   ├── templates/        # HTML 模板
│   └── static/           # 静态资源
│       ├── css/
│       ├── js/
│       └── images/
├── start.bat             # Windows 启动脚本
└── start.sh              # Linux/Mac 启动脚本
```

## 路由说明

### 前端页面
- `/` - 首页
- `/auth` - 登录/注册
- `/profile` - 个人主页
- `/search` - 搜索
- `/community` - 社区
- `/my-collections` - 我的收藏
- `/work-upload` - 作品上传
- `/work/<id>` - 作品详情
- `/review-center` - 审核中心

### API 接口
- `/api/auth/*` - 认证相关
- `/api/works/*` - 作品管理
- `/api/users/*` - 用户管理
- `/api/comments/*` - 评论管理
- `/api/collections/*` - 收藏管理

详细 API 文档：[Backend/README.md](Backend/README.md)

## 开发说明

### 数据模型
- **User**：用户（用户名、邮箱、头像、简介）
- **Work**：作品（标题、描述、图片、风格、审核状态）
- **Comment**：评论（支持回复）
- **Collection**：收藏
- **Like**：点赞

### 认证机制
使用 JWT Token 认证：
1. 登录后获取 `access_token` 和 `refresh_token`
2. 在请求头中添加：`Authorization: Bearer <access_token>`
3. Token 过期后使用 `refresh_token` 刷新

### 文件上传
- 支持格式：png, jpg, jpeg, gif, bmp
- 最大大小：16MB
- 上传目录：`Backend/uploads/`

## 常见问题

### 1. 端口被占用
修改 `Backend/app.py` 最后一行的端口号：
```python
app.run(host='0.0.0.0', port=5000, debug=True)
```

### 2. 数据库重置
删除 `Backend/icalligraphy.db` 文件，重新运行 `python init_db.py`

### 3. 依赖安装失败
尝试升级 pip：
```bash
pip install --upgrade pip
pip install -r Backend/requirements.txt
```

## 测试

使用 curl 或 Postman 测试 API：

```bash
# 注册
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser","email":"test@example.com","password":"password123"}'

# 登录
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"admin123"}'

# 获取作品列表
curl http://localhost:5000/api/works
```

## License

MIT
