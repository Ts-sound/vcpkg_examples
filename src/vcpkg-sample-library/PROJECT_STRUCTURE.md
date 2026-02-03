# vcpkg-sample-library Project Structure

本文档提供了 vcpkg-sample-library 项目的完整文件结构概览。

---

## 完整目录树

```bash
vcpkg-sample-library/
├── vcpkg.json                          # 端口清单文件
├── portfile.cmake                      # 端口构建脚本
├── usage                               # 使用说明文档
├── README.md                           # 端口概述文档
├── COMPLETE_GUIDE.md                   # 完整中文指南
├── PROJECT_STRUCTURE.md                # 本文档
│
├── example/                            # 使用示例项目
    ├── CMakeLists.txt                  # 示例项目构建配置
    ├── main.cpp                        # 示例应用程序
    ├── vcpkg.json                      # 示例项目依赖清单
    └── README.md                       # 示例项目详细说明

```

---

## 文件说明

### 端口核心文件

| 文件 | 大小 | 描述 |
|------|------|------|
| `vcpkg.json` | 小 | 端口元数据和依赖关系定义 |
| `portfile.cmake` | 中 | 构建、下载和安装的逻辑 |
| `usage` | 小 | 快速参考和 CMake 集成示例 |
| `README.md` | 大 | 详细的端口文档和教程 |

### 使用示例 (example/)

| 文件 | 描述 |
|------|------|
| `CMakeLists.txt` | 演示如何查找和链接库 |
| `main.cpp` | 演示如何使用库 API |
| `vcpkg.json` | 演示如何声明依赖 |
| `README.md` | 详细的构建和使用说明 |

### 库源代码 (example-port/)

- 查看 portfile.cmake
- github : MicrosoftDocs/vcpkg-docs

---

## 使用流程

### 1. 库作者创建端口

```bash
my_library_source/          →  创建 vcpkg 端口文件
    ├── CMakeLists.txt      →  portfile.cmake
    ├── include/            →  vcpkg.json
    └── src/                →  usage
```

### 2. 用户使用库

```bash
vcpkg install vcpkg-sample-library
    ↓
下载源代码
    ↓
构建库
    ↓
安装库文件和配置
    ↓
用户在项目中 find_package() 和 target_link_libraries()
```

---

## 关键技术栈

- **vcpkg**: 包管理器
- **CMake**: 构建系统
- **fmt**: 字符串格式化库（依赖）
- **C++11**: 最小语言标准

---

## 版本信息

- **端口版本**: 1.0.2
- **CMake 最低版本**: 3.10
- **C++ 最低标准**: C++11

---
