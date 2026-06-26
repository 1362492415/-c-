
# FlashProgrammer 多通道烧录上位机

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![.NET Version](https://img.shields.io/badge/.NET-10.0-purple.svg)](https://dotnet.microsoft.com/)
[![Platform](https://img.shields.io/badge/platform-Windows%2010+-lightgrey.svg)](https://www.microsoft.com/windows)

&gt; 一个功能强大的工业级多通道烧录上位机软件，支持批量芯片烧录、二维码追溯和进度实时监控

## 🚀 功能特点

| 功能 | 描述 |
|------|------|
| 🔥 **多通道烧录** | 支持最多 12 个通道同时烧录，大幅提高生产效率 |
| 📱 **二维码扫描** | 支持扫码枪和摄像头扫码，二维码自动校验，防止重复烧录 |
| 📊 **实时进度监控** | 各通道独立进度条，实时显示擦除、烧录、校验状态 |
| 📈 **数据追溯** | 集成 SQL Server，记录每片产品的烧录历史、状态码和时间信息 |
| 🔗 **硬件握手** | 完善的握手机制，确保通信可靠 |
| 🎨 **界面友好** | 现代化 WinForms 界面，操作简单直观 |

## 🛠️ 技术栈

![C#](https://img.shields.io/badge/C%23-239120?style=for-the-badge&amp;logo=c-sharp&amp;logoColor=white)
![.NET](https://img.shields.io/badge/.NET-5C2D91?style=for-the-badge&amp;logo=.net&amp;logoColor=white)
![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&amp;logo=windows&amp;logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL_Server-CC2927?style=for-the-badge&amp;logo=microsoft-sql-server&amp;logoColor=white)

| 技术 | 版本 |
|------|------|
| .NET | 10.0 |
| 界面框架 | Windows Forms |
| 数据库 | SQL Server |
| 串口通信 | System.IO.Ports |
| 二维码处理 | ZXing.Net |
| 视频采集 | AForge.Video |

## 📦 快速开始

### 环境要求

- ✅ Windows 10 或更高版本
- ✅ .NET 10.0 运行时
- ✅ SQL Server (可选，用于数据追溯功能)

### 编译运行

1. 克隆仓库到本地
   ```bash
   git clone https://github.com/你的用户名/FlashProgrammer.git
   cd FlashProgrammer
   ```

2. 使用 Visual Studio 2022 (或更高版本) 打开项目

3. 还原 NuGet 包
   ```bash
   dotnet restore
   ```

4. 按 F5 编译并运行

### 配置说明

在 `appsettings.json` 文件中配置以下参数：

```json
{
  "EnabledChannels": 12,           // 启用的通道数 (1-12)
  "GridColumns": 4,                // 界面网格列数
  "ShowQrCode": true,              // 是否显示二维码
  "DefaultPort": null,             // 默认串口
  "DefaultBaudRate": 115200,       // 默认波特率
  "TraceabilityConnectionString": "Server=YOUR_SQL_SERVER;Database=FlashProgrammer;User ID=YOUR_USER;Password=YOUR_PASSWORD;TrustServerCertificate=True;",
  "AutoOpenNextBatchScanAfterComplete": false
}
```

## 📖 使用说明

### 基本操作流程

1. **连接设备**
   - 选择串口和波特率
   - 点击「连接」按钮
   - 等待握手成功（界面提示「设备已就绪」）

2. **录入二维码**
   - 点击单通道的「扫码」按钮进行单独扫码
   - 或点击「批量扫码并启动」进行批量录入

3. **启动烧录**
   - 单通道：点击通道上的「启动烧录」按钮
   - 批量模式：点击「启动全部」

4. **查看历史**
   - 点击「追溯查询」按钮，输入二维码查看烧录历史

## 📂 项目结构

```
FlashProgrammer/
├── Form1.cs                    # 主窗体，核心业务逻辑
├── ChannelControl.cs           # 通道控件
├── SerialCommunicator.cs       # 串口通信层
├── Protocol.cs                 # 协议解析与封装
├── Traceability.cs             # 追溯数据库操作
├── QrCodeScanner.cs            # 二维码扫描
├── Logger.cs                   # 日志记录
├── Program.cs                  # 程序入口
└── FlashProgrammer.csproj      # 项目配置
```

## 💾 数据库

首次运行时，程序会自动在 SQL Server 中创建 `BurnRecords` 表，用于记录烧录历史。

### 表结构说明

| 字段 | 类型 | 说明 |
|------|------|------|
| `Id` | BIGINT | 主键自增 |
| `QrCode` | NVARCHAR(200) | 产品二维码 |
| `ChannelNumber` | INT | 通道号 |
| `Result` | NVARCHAR(32) | 烧录结果 (Success/Failed) |
| `StatusCode` | NVARCHAR(32) | 状态码 |
| `StatusText` | NVARCHAR(128) | 状态文字说明 |
| `StartTime` | DATETIME2 | 开始时间 |
| `EndTime` | DATETIME2 | 结束时间 |
| `DurationMs` | BIGINT | 耗时 (毫秒) |
| `DeviceInfo` | NVARCHAR(512) | 设备信息 |
| `FirmwareName` | NVARCHAR(260) | 固件名称 |
| `PortName` | NVARCHAR(64) | 串口名称 |
| `BatchId` | NVARCHAR(64) | 批次号 |
| `ErrorMessage` | NVARCHAR(512) | 错误信息 |
| `CreatedAt` | DATETIME2 | 记录创建时间 |
| `IsBatch` | BIT | 是否批量烧录 |

## 📝 许可证

本项目仅供学习和研究使用。

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

---

&lt;div align="center"&gt;
  &lt;strong&gt;Made with ❤️ by Your Name&lt;/strong&gt;
&lt;/div&gt;
