# PandaTalk 绕口令语音评测系统

基于讯飞语音评测API的智能绕口令练习和评测系统，为PandaTalk应用提供专业的普通话发音训练功能。

## 🎯 项目概述

本项目为PandaTalk应用开发绕口令功能模块，通过集成讯飞语音评测API，为用户提供：

- 🎪 **丰富的绕口令文本库** - 涵盖初级到高级，声母韵母到综合练习
- 🎤 **实时语音录制和评测** - 支持实时录音，即时获得评测结果
- 📊 **多维度发音分析** - 发音准确度、流畅度、完整性、语调四维评分
- 💡 **个性化练习建议** - 基于评测结果提供针对性改进建议
- 📈 **历史记录管理** - 跟踪练习进度，分析提升趋势

## ✨ 核心功能

### 1. 智能语音评测
- 🔗 基于讯飞语音评测API，专业可靠
- 🎵 支持实时录音和音频文件上传
- 📏 多维度评分：发音准确度、流畅度、完整性、语调自然度
- 💬 详细的反馈和个性化改进建议
- ⚡ 快速响应，评测结果秒级返回

### 2. 分级绕口令库
- 📚 **按难度分级**：初级(7个)、中级(5个)、高级(5个)
- 🎭 **按类型分类**：声母练习、韵母练习、声调练习、综合练习
- 🔍 **智能搜索**：支持关键词搜索，快速定位目标练习
- 🎲 **随机推荐**：可按难度随机推荐，保持练习新鲜感
- 📋 **个性化序列**：根据用户水平推荐最适合的练习顺序

### 3. 专业音频处理
- 🔄 自动音频格式转换（转换为16kHz, 16bit, 单声道PCM）
- 🎚️ 音频质量优化（音量标准化、降噪处理）
- ✂️ 智能静音检测和裁剪
- 📱 多设备音频输入支持

### 4. 智能评分系统
- 🧠 基于讯飞专业算法的评分引擎
- 📊 历史记录分析和进步趋势跟踪
- 🏆 等级评定：优秀(90+)、良好(80+)、中等(70+)、及格(60+)
- 📝 详细的单词级别评分反馈

## 🏗️ 技术架构

```
speech_evaluation/
├── config/                    # 配置管理
│   └── xfyun_config.py       # 讯飞API配置和认证
├── src/                      # 核心源代码
│   ├── api/                  # API客户端层
│   │   └── xfyun_client.py   # 讯飞WebSocket客户端
│   ├── audio/                # 音频处理层
│   │   └── audio_processor.py # 音频录制、转换、预处理
│   ├── scoring/              # 评分引擎层
│   │   └── score_engine.py   # 结果解析、评分、反馈生成
│   ├── utils/                # 工具模块
│   │   └── twister_library.py # 绕口令文本库管理
│   └── twister_evaluator.py  # 主评测控制器
├── tests/                    # 单元测试
│   └── test_basic.py         # 基础功能测试
├── examples/                 # 使用示例
│   └── basic_usage.py        # 完整的交互式演示程序
├── docs/                     # 项目文档
└── requirements.txt          # Python依赖包列表
```

## 🚀 快速开始

### 环境要求
- Python 3.7+
- Windows/macOS/Linux
- 麦克风设备
- 网络连接（用于API调用）

### 安装步骤

1. **克隆项目**
```bash
git clone <repository-url>
cd speech_evaluation
```

2. **安装依赖**
```bash
pip install -r requirements.txt
```

3. **配置API密钥**

获取讯飞API密钥：
1. 访问 [讯飞开放平台](https://console.xfyun.cn/)
2. 注册并登录账号
3. 创建应用，获取 APPID、API_SECRET、API_KEY

配置方式（选择其一）：

**方式一：使用配置脚本（推荐）**
```bash
python demo_config.py
```
按提示输入您的API密钥，脚本会自动创建 `config/api_keys.py` 文件。

**方式二：手动配置**
1. 复制 `config/api_keys.example.py` 为 `config/api_keys.py`
2. 编辑 `config/api_keys.py`，填入您的真实API密钥

**注意：** `api_keys.py` 文件已被添加到 `.gitignore`，不会被上传到版本控制系统，保护您的API密钥安全。

4. **运行示例程序**
```bash
python examples/basic_usage.py
```

### 获取讯飞API密钥

1. 访问 [讯飞开放平台](https://www.xfyun.cn/)
2. 注册账号并登录
3. 创建应用，选择"语音评测"服务
4. 获取APPID、API_SECRET、API_KEY
5. 将凭证填入配置文件

## 📖 使用指南

### 基础使用

```python
from src.twister_evaluator import TwisterEvaluator
from src.utils.twister_library import TwisterLibrary

# 初始化系统
evaluator = TwisterEvaluator()
library = TwisterLibrary()

# 获取绕口令
twister = library.get_random_twister('初级')
print(f"练习内容: {twister['text']}")

# 开始评测
result = await evaluator.evaluate_speech(
    text=twister['text'],
    duration=5  # 录音时长（秒）
)

# 查看结果
print(f"总分: {result.overall_score}分")
print(f"等级: {result.grade}")
```

### 交互式程序

运行完整的交互式演示程序：

```bash
python examples/basic_usage.py
```

程序提供以下功能：
- 📚 浏览绕口令库（按难度、类别、搜索）
- 🎤 语音评测（选择绕口令、录音、查看结果）
- 📊 历史记录查看
- ⚙️ 系统信息显示

### 绕口令库使用

```python
from src.utils.twister_library import TwisterLibrary

library = TwisterLibrary()

# 按难度获取
beginner_twisters = library.get_twisters_by_difficulty('初级')

# 按类别获取
consonant_twisters = library.get_twisters_by_category('声母练习')

# 搜索绕口令
results = library.search_twisters('四是四')

# 获取推荐序列
sequence = library.get_recommended_sequence('初级')
```

## 🧪 测试

运行单元测试：

```bash
# 运行所有测试
python -m pytest tests/ -v

# 运行特定测试
python -m pytest tests/test_basic.py::TestTwisterLibrary -v

# 查看测试覆盖率
pip install pytest-cov
python -m pytest tests/ --cov=src --cov-report=html
```

## 📋 开发计划

### ✅ 第一阶段：基础框架（已完成）
- [x] 项目结构搭建和模块化设计
- [x] 讯飞语音评测API集成
- [x] WebSocket通信和认证机制
- [x] 音频录制和格式转换
- [x] 评分引擎和结果解析
- [x] 绕口令文本库（17个精选绕口令）
- [x] 完整的示例程序和测试用例

### 🔄 第二阶段：功能完善（进行中）
- [ ] 绕口令库扩充至50+个
- [ ] 图形用户界面开发
- [ ] 数据库集成和历史记录持久化
- [ ] 性能优化和错误处理增强
- [ ] 音频质量检测和自动重录

### 🎯 第三阶段：高级功能（规划中）
- [ ] 基于AI的个性化推荐算法
- [ ] 社交分享和排行榜功能
- [ ] 多语言支持（方言、外语）
- [ ] 离线模式和本地评测
- [ ] 移动端适配和优化

## 🛠️ 故障排除

### 常见问题

**1. PyAudio安装失败**
```bash
# Windows
pip install pipwin
pipwin install pyaudio

# macOS
brew install portaudio
pip install pyaudio

# Ubuntu/Debian
sudo apt-get install python3-pyaudio
```

**2. 麦克风权限问题**
- 确保应用有麦克风访问权限
- 检查系统音频设备设置
- 运行 `python -c "import pyaudio; print('PyAudio OK')"`

**3. API调用失败**
- 检查网络连接
- 验证API密钥是否正确
- 确认讯飞账户余额充足

**4. 音频质量问题**
- 使用质量较好的麦克风
- 在安静环境中录音
- 调整录音音量到适中水平

### 调试模式

启用详细日志输出：

```python
import logging
logging.basicConfig(level=logging.DEBUG)
```

## 🤝 贡献指南

欢迎贡献代码、报告问题或提出建议！

1. Fork 项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

### 代码规范
- 使用 Black 进行代码格式化
- 遵循 PEP 8 编码规范
- 添加适当的注释和文档字符串
- 编写单元测试覆盖新功能

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

## 🙏 致谢

- [讯飞开放平台](https://www.xfyun.cn/) - 提供专业的语音评测API
- [PyAudio](https://pypi.org/project/PyAudio/) - Python音频处理库
- [WebSockets](https://pypi.org/project/websockets/) - WebSocket通信支持

## 📞 联系我们

如有问题或建议，请通过以下方式联系：

- 📧 Email: [your-email@example.com]
- 🐛 Issues: [GitHub Issues页面]
- 💬 讨论: [GitHub Discussions页面]

---

**PandaTalk绕口令语音评测系统** - 让普通话学习更有趣、更高效！ 🎉