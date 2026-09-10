# 像素动画序列帧生成系统

基于 OpenAI Codex 的智能像素动画生成工具，支持一键生成攻击、待机、行走、技能动画序列帧，直接导入Godot引擎。

## 🎮 核心功能

- ✨ **Codex驱动生成** - 使用OpenAI Codex生成自适应的像素处理代码
- 🎬 **多动作支持** - 攻击、待机、行走、技能4种连贯动作
- 🎨 **像素风格保持** - 基于参考图自动适配像素风格和调色板
- 📦 **Godot集成** - 直接导出SpriteSheet + AnimationPlayer配置
- 🔄 **GitHub Actions** - 自动化生成工作流
- 🌊 **动作连贯性** - 帧间平滑过渡，保证流畅动画

## 📋 工作流程

```
参考图输入
    ↓
Codex分析特征 + 生成处理代码
    ↓
执行生成代码生成序列帧
    ↓
帧间插值(确保连贯)
    ↓
打包SpriteSheet + 生成Godot资源文件
    ↓
Godot项目导出完成
```

## 🚀 快速开始

### 环境要求
- Python 3.9+
- OpenAI API Key (Codex访问权限)
- Godot 4.0+ (可选，仅用于验证)

### 安装依赖
```bash
pip install -r requirements.txt
```

### 基本使用
```bash
# 1. 配置API Key
export OPENAI_API_KEY="your-api-key"

# 2. 放置参考图到 input/reference.png
cp your_reference.png input/reference.png

# 3. 运行生成
python main.py --config config.json

# 4. 查看输出
# output/sprite_sheet.png - 完整SpriteSheet
# output/animation_config.json - Godot动画配置
# output/godot_resource.tres - Godot资源文件
```

## 📁 项目结构

```
pixel-animation-generator/
├── main.py                 # 主程序入口
├── requirements.txt        # Python依赖
├── config.json            # 配置文件
├── src/
│   ├── codex_agent.py     # Codex集成模块
│   ├── reference_analyzer.py # 参考图分析
│   ├── frame_generator.py  # 序列帧生成
│   ├── interpolator.py     # 帧间插值
│   └── godot_exporter.py   # Godot资源导出
├── input/                 # 输入目录（放参考图）
├── output/                # 输出目录（生成结果）
└── .github/workflows/
    └── generate.yml       # GitHub Actions工作流
```

## 🔧 配置说明

编辑 `config.json`:
```json
{
  "reference_image": "input/reference.png",
  "pixel_size": 16,
  "output_width": 512,
  "output_height": 512,
  "animations": {
    "idle": {
      "frames": 4,
      "fps": 8,
      "loop": true
    },
    "walk": {
      "frames": 6,
      "fps": 10,
      "loop": true
    },
    "attack": {
      "frames": 5,
      "fps": 12,
      "loop": false
    },
    "skill": {
      "frames": 8,
      "fps": 12,
      "loop": false
    }
  },
  "codex_model": "code-davinci-002",
  "interpolation_frames": 2
}
```

## 🎯 工作流触发方式

### GitHub Actions 触发
```bash
# 推送含 reference.png 的提交
git add input/reference.png
git commit -m "New reference: knight character"
git push

# 自动触发 generate.yml 工作流
# 生成结果自动上传到 Releases
```

### 本地执行
```bash
python main.py --config config.json --output output/
```

## 📊 动作连贯性保证

1. **Codex代码生成** - 生成帧间过渡逻辑
2. **光流插值** - 使用RIFE进行中间帧生成
3. **循环缝合** - 首尾帧自动融合
4. **动作衔接** - idle→walk→attack→skill 智能过渡

## 🎨 支持的特性

- ✅ 多种像素尺寸 (8x8, 16x16, 32x32)
- ✅ 自动调色板检测
- ✅ 骨架动画支持 (可选)
- ✅ 背景透明度保持
- ✅ 多种导出格式 (PNG, ASEPRITE, Godot)

## 📝 API文档

详见 [API.md](./docs/API.md)

## 🤝 贡献

欢迎提交Issue和Pull Request！

## 📄 许可证

MIT License

## 💬 反馈

有任何问题或建议，欢迎在Issues中讨论！
