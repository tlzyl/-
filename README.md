# HIS 重写版

该目录是新交付工程，未改动原 `hisclient` 和 `hismodules`。

## 技术栈

- 前端：Vue 3、Vite、Element Plus、Axios、Vue Router
- 后端：Spring Boot 3、MyBatis-Plus、MySQL
- 删除策略：主业务表均包含 `deleted` 字段，并启用 MyBatis-Plus 逻辑删除
- 后端启动时会自动检查旧库表结构，补齐缺失表和 `deleted` 字段，兼容已有的 `his01` 数据库。

## 启动步骤

1. 初始化数据库

```sql
source C:/Users/zzy74/Downloads/shixunclassdisgn/his-rewrite/database/init.sql;
```

2. 启动后端

```bash
cd C:/Users/zzy74/Downloads/shixunclassdisgn/his-rewrite/backend
mvn spring-boot:run
```

默认连接 `127.0.0.1:3306/his01`，账号密码在 `backend/src/main/resources/application.yml`。
后端工程使用 Java 17，IDEA 中请将 Project SDK 和 Maven Runner JRE 都设置为 JDK 17。

也可以在 PowerShell 里运行：

```powershell
.\start-backend.ps1
```

3. 启动前端

```bash
cd C:/Users/zzy74/Downloads/shixunclassdisgn/his-rewrite/frontend
pnpm install
pnpm dev
```

浏览器打开 `http://localhost:5173`。

也可以在 PowerShell 里运行：

```powershell
.\start-frontend.ps1
```

## 已保留的原功能入口

- 挂号收费：窗口挂号、窗口退号、收费、退费、费用记录查询
- 门诊医生：患者查看、医生诊疗、看诊记录
- 检验：检验申请、患者录入、检验结果录入、检验管理
- 处置管理：处置申请、患者录入、处置录入、处置管理
- 药房管理：药房发药、药房退药、交易记录
- 检查：检查申请、患者录入、结果录入、检查管理

## 兼容旧接口

后端保留了旧项目前端使用的接口路径，例如：

- `GET /getRegistLevelList`
- `GET /getAllDeptList`
- `GET /getSettleCategory`
- `GET /getRegistDoctorList`
- `GET /getMaxCaseNumber`
- `GET /getAlreadyRegisterCount`
- `POST /addRegister`

同时新增了更清晰的 `/api/...` 接口供 Vue3 前端使用。
