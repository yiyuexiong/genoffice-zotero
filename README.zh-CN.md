# GenOffice Zotero Integration

[English](README.md)

> [!IMPORTANT]
> 这是基于 GenOffice 的非官方派生项目，与 GenOffice、Genspark 或 Zotero 没有隶属或背书关系。
> 当前版本为 Alpha 预览版，仅供测试与评估，请勿用于重要或生产文档。

## 项目简介

GenOffice Zotero Integration 是基于
[GenOffice v0.9.10](https://github.com/genspark-ai/genoffice/tree/v0.9.10) 的非官方定制版，
目标是让用户在 GenOffice Docs 中像使用 Word 或 WPS 一样使用 Zotero。

本分支保留完整 GenOffice 应用壳，业务修改集中在 `apps/docs` 和
`packages/docx-engine` 的 Zotero 接入与 DOCX 往返兼容。

![GenOffice Docs 中的 Zotero 工具组](docs/assets/current-reference-tab.png)

## 已实现功能

- 使用 Zotero LibreOffice Integration API v3 与 Zotero 桌面端通信。
- 添加或编辑正文引文、参考文献表，并刷新它们。
- 设置 Zotero 文档首选项，或移除域代码并保留可见文本。
- 保留 Word `ADDIN ZOTERO_*` 字段和 `ZOTERO_PREF_1..n` 自定义属性。
- 支持跨段落参考文献表，每个条目独立成段。
- 支持 Zotero RTF 中常用的粗体、斜体、下划线、删除线、上下标、字号和大小写样式。
- 支持文献表的悬挂缩进、段落间距和对齐。
- 保留 GenOffice 浅色、深色和跟随系统主题。

## 下载与安装

当前只提供在 Intel Mac 上构建的未签名测试包：

1. 从 [Releases](https://github.com/yiyuexiong/genoffice-zotero/releases) 下载
   `GenOffice-Zotero-Intel-macOS.zip`。
2. 解压后将 `GenOffice.app` 移到“应用程序”。
3. 启动 Zotero 桌面端，再启动 GenOffice。
4. macOS 如果拦截未签名应用，请在“系统设置 → 隐私与安全性”中确认打开。

已验证环境：Zotero 9.0.6、macOS Intel x86_64、GenOffice v0.9.10。
Apple Silicon、Windows 和 Linux 用户目前需要从源码构建（Sorry，我现在手上没有 Apple Silicon、Windows 或者 Linux 的电脑）。

## 使用方法

1. 先启动 Zotero。
2. 在 GenOffice 中打开或新建 `.docx` 文档。
3. 打开“引用”选项卡。
4. 使用“Zotero 引文”、“Zotero 文献表”、“刷新”或“文档首选项”。
5. 保存为 DOCX，Zotero 域代码会与可见内容一起保存。

![GenOffice Zotero 操作示范](docs/assets/zotero-operation-demo.gif)

GenOffice 通过 `127.0.0.1:23116` 与本机 Zotero 通信，不直接读取或修改
Zotero 数据库。

## 从源码构建

要求 Node.js 22.12 或更高版本、npm 10 或更高版本。

```bash
npm install
npm run dev
```

构建 Docs 和完整 GenOffice 壳：

```bash
npm run build -w @genoffice/docs
npm run build -w @genoffice/shell
```

运行核心测试：

```bash
npm run test -w @genoffice/docs
npm run test -w @genoffice/docx-engine
npm run typecheck -w @genoffice/docs
npm run typecheck -w @genoffice/docx-engine
```

当前验证基线：Docs 1525 项通过；DOCX 引擎 1001 项通过、1 项跳过。

## 已知限制

- 脚注式和尾注式 Zotero 引文尚未实现。
- RTF 字体表、颜色和复杂嵌入对象尚未映射。
- Zotero 文档迁移、placeholder 转换以及 export/import 尚未实现。
- 当前 macOS 包仅为 Intel x86_64，且未签名、未公证。

## 上游、许可证与商标

本项目基于 [genspark-ai/genoffice](https://github.com/genspark-ai/genoffice)，原版 README 保存在
[README-GENOFFICE.md](README-GENOFFICE.md)。本仓库保留原项目的
[Apache License 2.0](LICENSE)、[NOTICE](NOTICE) 和第三方声明；`ee/` 目录受其独立许可证约束。

GenOffice 和 Genspark 名称及标志是 Mainfunc, Inc. 的商标；Apache-2.0 不授予商标使用权。
Zotero 是 Corporation for Digital Scholarship 的商标。本项目与上述任何组织均无隶属或背书关系。
在公开发布派生应用前，应替换原 GenOffice 名称和图标，并完成独立的签名与公证。

