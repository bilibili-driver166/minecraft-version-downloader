# Minecraft 全版本下载器 · 单文件源码版

这是把下载器所有 Python 代码合并后的**单个源码文件**，不依赖 `mcdl/` 包，也不依赖外部 `version_manifest_v2.json`（清单已压缩内嵌）。

## 文件

```text
mc_downloader_single.py   # 全部代码，可直接运行/打包
icon.ico                  # exe 图标
icon.png                  # 图标预览
version_info.txt          # PyInstaller 版本信息
build_single.bat          # 一键打包单文件 exe
```

## 直接运行

```bash
python mc_downloader_single.py
```

## 打包单文件 exe

```bat
python -m pip install pyinstaller
build_single.bat
```

等价命令：

```bat
python -m PyInstaller --noconfirm --clean --onefile --windowed ^
  --name "Minecraft全版本下载器" ^
  --icon "icon.ico" ^
  --version-file "version_info.txt" ^
  --paths . mc_downloader_single.py
```

输出：`dist\Minecraft全版本下载器.exe`

因为没有额外的 `--add-data`，打包时不需要携带 `data` 目录。

注意：PyInstaller 的 `--onefile` 在运行时会把运行库解压到 `%TEMP%\_MEI...`。如果目标机器的临时目录不可写，请改用 `--onedir` 打包，或参考多文件源码包中的便携版方案。

## 已包含

- Mojang 全版本、Fabric / Forge / NeoForge 安装、愚人节版本
- SHA-1 校验、断点式 `.part` 下载、natives、旧版资源映射
- 内置 920 个版本的离线清单种子
- Java 自动检测、缓存回退、异步 Tkinter 界面
