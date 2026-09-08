# GenOffice Zotero Integration

[中文](#中文) | [English](#english)

> [!IMPORTANT]
> This is an unofficial derivative project based on GenOffice. It is not affiliated with or
> endorsed by GenOffice, Genspark, or Zotero. The current build is an alpha preview for private
> review.

## 中文

### 项目简介

GenOffice Zotero Integration 是基于
[GenOffice v0.9.10](https://github.com/genspark-ai/genoffice/tree/v0.9.10) 的非官方定制版，
目标是让用户在 GenOffice Docs 中像使用 Word 或 WPS 一样使用 Zotero。

本分支保留完整 GenOffice 应用壳，业务修改集中在 `apps/docs` 和
`packages/docx-engine` 的 Zotero 接入与 DOCX 往返兼容。

![GenOffice Docs 中的 Zotero 工具组](docs/assets/current-reference-tab.png)

### 已实现功能

- 使用 Zotero LibreOffice Integration API v3 与 Zotero 桌面端通信。
- 添加或编辑正文引文、参考文献表，并刷新它们。
- 设置 Zotero 文档首选项，或移除域代码并保留可见文本。
- 保留 Word `ADDIN ZOTERO_*` 字段和 `ZOTERO_PREF_1..n` 自定义属性。
- 支持跨段落参考文献表，每个条目独立成段。
- 支持 Zotero RTF 中常用的粗体、斜体、下划线、删除线、上下标、字号和大小写样式。
- 支持文献表的悬挂缩进、段落间距和对齐。
- 保留 GenOffice 浅色、深色和跟随系统主题。

### 下载与安装

当前只提供在 Intel Mac 上构建的未签名测试包：

1. 从 [Releases](https://github.com/yiyuexiong/genoffice-zotero/releases) 下载
   `GenOffice-Zotero-Intel-macOS.zip`。
2. 解压后将 `GenOffice.app` 移到“应用程序”。
3. 启动 Zotero 桌面端，再启动 GenOffice。
4. macOS 如果拦截未签名应用，请在“系统设置 → 隐私与安全性”中确认打开。

已验证环境：Zotero 9.0.6、macOS Intel x86_64、GenOffice v0.9.10。
Apple Silicon、Windows 和 Linux 用户目前需要从源码构建。

### 使用方法

1. 先启动 Zotero。
2. 在 GenOffice 中打开或新建 `.docx` 文档。
3. 打开“引用”选项卡。
4. 使用“Zotero 引文”、“Zotero 文献表”、“刷新”或“文档首选项”。
5. 保存为 DOCX，Zotero 域代码会与可见内容一起保存。

GenOffice 通过 `127.0.0.1:23116` 与本机 Zotero 通信，不直接读取或修改
Zotero 数据库。

### 从源码构建

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

### 已知限制

- 脚注式和尾注式 Zotero 引文尚未实现。
- `Document_setBibliographyStyle` 尚未完整映射；RTF 自带的段落样式已支持。
- RTF 字体表、颜色和复杂嵌入对象尚未映射。
- Zotero 文档迁移、placeholder 转换以及 export/import 尚未实现。
- 尚未完成 Word、WPS 和 GenOffice 三方人工往返测试矩阵。
- 当前 macOS 包仅为 Intel x86_64，且未签名、未公证。

### 上游、许可证与商标

本项目基于 [genspark-ai/genoffice](https://github.com/genspark-ai/genoffice)，原版 README 保存在
[README-GENOFFICE.md](README-GENOFFICE.md)。本仓库保留原项目的
[Apache License 2.0](LICENSE)、[NOTICE](NOTICE) 和第三方声明；`ee/` 目录受其独立许可证约束。

GenOffice 和 Genspark 名称及标志是 Mainfunc, Inc. 的商标；Apache-2.0 不授予商标使用权。
Zotero 是 Corporation for Digital Scholarship 的商标。本项目与上述任何组织均无隶属或背书关系。
在公开发布派生应用前，应替换原 GenOffice 名称和图标，并完成独立的签名与公证。

---

## English

### Overview

GenOffice Zotero Integration is an unofficial derivative of
[GenOffice v0.9.10](https://github.com/genspark-ai/genoffice/tree/v0.9.10). Its goal is to make
Zotero available inside GenOffice Docs with a workflow similar to the Zotero integrations for
Microsoft Word and WPS Office.

The branch keeps the complete GenOffice application shell. Product changes are scoped to Zotero
integration in `apps/docs` and Zotero-compatible DOCX round trips in `packages/docx-engine`.

### Implemented

- Communication with Zotero Desktop through Zotero LibreOffice Integration API v3.
- Add, edit, and refresh in-text citations and bibliographies.
- Open Zotero document preferences or remove field codes while retaining visible text.
- Preserve Word `ADDIN ZOTERO_*` fields and `ZOTERO_PREF_1..n` custom properties.
- Preserve one logical Zotero bibliography field across multiple paragraphs.
- Split Zotero bibliography entries into separate paragraphs.
- Map common Zotero RTF formatting: bold, italic, underline, strike-through, superscript,
  subscript, font size, and capitalization.
- Map hanging indents, paragraph spacing, and alignment.
- Preserve the original GenOffice light, dark, and system themes.

### Download and installation

The current release is an unsigned test build produced on an Intel Mac:

1. Download `GenOffice-Zotero-Intel-macOS.zip` from
   [Releases](https://github.com/yiyuexiong/genoffice-zotero/releases).
2. Extract it and move `GenOffice.app` to Applications.
3. Start Zotero Desktop before starting GenOffice.
4. If macOS blocks the unsigned application, confirm it under System Settings > Privacy &
   Security.

Verified environment: Zotero 9.0.6, macOS Intel x86_64, and GenOffice v0.9.10.
Apple Silicon, Windows, and Linux users currently need to build from source.

### Usage

1. Start Zotero.
2. Open or create a `.docx` document in GenOffice.
3. Open the References tab.
4. Use Zotero Citation, Zotero Bibliography, Refresh, or Document Preferences.
5. Save as DOCX. Zotero field codes are stored together with their visible content.

GenOffice communicates with the local Zotero process through `127.0.0.1:23116`. It does not read
or modify the Zotero database directly.

### Build from source

Node.js 22.12 or newer and npm 10 or newer are required.

```bash
npm install
npm run dev
```

Build Docs and the complete GenOffice shell:

```bash
npm run build -w @genoffice/docs
npm run build -w @genoffice/shell
```

Run the core checks:

```bash
npm run test -w @genoffice/docs
npm run test -w @genoffice/docx-engine
npm run typecheck -w @genoffice/docs
npm run typecheck -w @genoffice/docx-engine
```

Current verified baseline: 1525 Docs tests passed; 1001 DOCX engine tests passed and 1 skipped.

### Known limitations

- Zotero footnote and endnote citations are not implemented.
- `Document_setBibliographyStyle` is not fully mapped; paragraph formatting included in RTF is
  supported.
- RTF font tables, colors, and complex embedded objects are not mapped.
- Zotero document migration, placeholder conversion, and export/import are not implemented.
- A manual Word, WPS, and GenOffice round-trip matrix has not been completed.
- The current macOS build is Intel x86_64 only, unsigned, and not notarized.

### Upstream, license, and trademarks

This project is based on [genspark-ai/genoffice](https://github.com/genspark-ai/genoffice). The
original README is preserved at [README-GENOFFICE.md](README-GENOFFICE.md). This repository retains the
upstream [Apache License 2.0](LICENSE), [NOTICE](NOTICE), and third-party notices. The `ee/`
directory is governed by its separate license.

The GenOffice and Genspark names and logos are trademarks of Mainfunc, Inc.; Apache-2.0 does not
grant trademark rights. Zotero is a trademark of the Corporation for Digital Scholarship. This
project is not affiliated with or endorsed by any of these organizations. Before publicly
distributing the derivative application, replace the original GenOffice name and icon and complete
independent code signing and notarization.

## Development status

The published branch is `main`, based on GenOffice v0.9.10 commit `f2c3d08`. The next priority is a
real Word, WPS, and GenOffice citation and bibliography round-trip matrix.
