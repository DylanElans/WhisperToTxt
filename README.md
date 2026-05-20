#  WhisperToTxt

将 MP4 视频转换为文字内容的工具（基于 whisper.cpp），  
同时提供视频转码（H.264）功能，用于解决部分设备（如 TV）播放 MP4 有声音无图像的问题。

---

## ✨ 功能

- 🎙 视频转文字（支持中文）
- 📁 支持单文件 / 整个目录（递归）
- 📂 支持指定输出目录，并保留输入目录的子目录结构
- ⏱ 可统计音频时长
- 🧹 文本清洗功能
- 🎬 MP4 转 H.264 编码（兼容性更好）


## ✨ 适用场景
- 视频字幕提取
- 会议记录
- 学习笔记整理
- 音频内容归档


---

##  使用环境：  Windows10 或以上的 DOS窗口 （CMD）

## 📦 依赖环境

### 1️⃣ Whisper 模型（必须）

下载地址：

whisper: https://huggingface.co/ggerganov/whisper.cpp/tree/main

推荐模型：

- ggml-small-q8_0.bin（速度快）
- ggml-large-v3-turbo.bin（精度高）

放入目录：

models/

---

### 2️⃣ 工具依赖

需要以下文件：

- ffmpeg.exe
- ffprobe.exe
- whisper-cli.exe

下载地址：

- ffmpeg: https://www.gyan.dev/ffmpeg/builds/


---

## 📁 目录结构

```text
project/
├─ transcribe.bat
├─ changeCodeH264.bat
├─ models/
│  ├─ ggml-small-q8_0.bin
│  └─ ggml-large-v3-turbo.bin
├─ ffmpeg.exe
├─ ffprobe.exe
├─ whisper-cli.exe
├─ input/
└─ output/            # 默认输出目录
```
---

## 🚀 使用方法

### 🎙 视频转文字

#### 单文件

```bash
transcribe.bat "input\test.mp4"
```

#### 带参数

```bash
transcribe.bat "input\test.mp4" clean notime
```

#### 指定输出目录

第 1 个参数为输入文件 / 输入目录，第 2 个参数为输出目录：

```bash
transcribe.bat "input\test.mp4" "D:\txt_output" notime clean
```

如果第 2 个参数是 `duration` / `small` / `large` / `notime` / `clean`，则会被识别为功能参数，不会被当作输出目录。

---

### 📁 处理整个目录（递归）

```bash
transcribe.bat "input\"
```

#### 递归处理并指定输出目录

```bash
transcribe.bat "input\" "D:\txt_output" notime clean
```

处理目录时会保留输入目录下的子目录结构，例如：

```text
input\A\test.mp4
```

会输出到：

```text
D:\txt_output\A\test.txt
```

---

### ⏱ 时长统计模式

```bash
transcribe.bat "input\test.mp4" duration
```

也可以统计整个目录：

```bash
transcribe.bat "input\" duration
```

---


## ⚙ 参数说明

| 参数 | 说明 |
|------|------|
| large | 使用大模型（默认） |
| small | 使用小模型 |
| duration | 统计时长 |
| notime | 不生成时间戳文件 |
| clean | 清洗文本 |
| 第 2 个参数为目录 | 指定输出目录，目录不存在时会自动创建 |

> 注意：如果不指定输出目录，默认输出到脚本所在目录下的 `output/`。


---

## 🎬 MP4 视频转码（H.264）

用于解决部分设备（如电视）播放 MP4 时“有声音无画面”的问题。

---

### 📌 使用方法

#### 1️⃣ 转换单个文件

```bash
changeCodeH264.bat "D:\test.mp4" "D:\NEW\"
```

---

#### 2️⃣ 批量处理目录（输出到新目录）

```bash
changeCodeH264.bat "D:\old" "D:\NEW\"
```

---

#### 3️⃣ 批量处理目录（原目录输出）

```bash
changeCodeH264.bat "D:\videos\"
```

---

### ⚙ 转码说明

- 使用 H.264 编码（高兼容性）
- 适用于 TV / 盒子 / 老设备
- 解决“音频正常但画面黑屏”的问题

---

## 📄 输出

输出目录：

- 默认输出到脚本所在目录下的 `output/`
- 也可以通过第 2 个参数指定输出目录

生成内容：

- 文本文件 `.txt`
- 时间轴文件 `_timed.txt`（使用 `notime` 参数时不生成）

目录模式下会保留子目录结构：

```text
input\课程1\a.mp4
```

输出为：

```text
output\课程1\a.txt
```

---

## 参考：完整的文件及目录图
![界面](images/filedir.png)

---

## 📄 License

MIT
