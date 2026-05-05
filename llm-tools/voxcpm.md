# VoxCPM

- **地址**：https://github.com/OpenBMB/VoxCPM
- **作者/团队**：OpenBMB（ModelBest + 清华大学 THUHCSI）
- **协议**：Apache-2.0
- **分类**：大模型工具

## 简介

OpenBMB 开源的无 Tokenizer 端到端 Text-to-Speech 系统，基于扩散自回归架构直接生成连续语音表示，绕过离散 Tokenization，实现高自然度、高表现力的语音合成。最新版 VoxCPM2 为 2B 参数模型，在超过 200 万小时多语言语音数据上训练，支持 30 种语言、Voice Design、可控语音克隆和 48kHz 录音棚级音质输出。基于 [MiniCPM-4](https://github.com/OpenBMB/MiniCPM) 骨干网络。

## 核心特性

- **30 语言多语种**：输入任意支持语言的文本即可合成，无需语言标签（含中日韩英法德西俄等，以及四川话、粤语、吴语等中国方言）
- **Voice Design**：通过自然语言描述（性别、年龄、音色、情感、语速等）创造全新声音，无需参考音频
- **可控语音克隆**：从短音频克隆音色，可选风格指导控制情感、语速和表现力，同时保留原始音色
- **终极克隆（Ultimate Cloning）**：提供参考音频及其转录文本，模型从参考处无缝延续，忠实复刻音色、节奏、情感、风格的每个细节
- **48kHz 高品质音频**：接受 16kHz 参考音频输入，通过 AudioVAE V2 的非对称编解码设计直接输出 48kHz 音质，内置超分辨率
- **实时流式推理**：RTX 4090 上 RTF 低至 ~0.3，Nano-vLLM 加速后 ~0.13
- **完全开源可商用**：Apache-2.0 协议，权重和代码全部开放

## 模型版本对比

| | VoxCPM2 | VoxCPM1.5 | VoxCPM-0.5B |
|---|:---:|:---:|:---:|
| **参数** | 2B | 0.6B | 0.5B |
| **采样率** | 48kHz | 44.1kHz | 16kHz |
| **语言** | 30 | 中/英 | 中/英 |
| **Voice Design** | ✅ | — | — |
| **可控克隆** | ✅ | — | — |
| **显存占用** | ~8 GB | ~6 GB | ~5 GB |
| **RTF (4090)** | ~0.30 | ~0.15 | ~0.17 |

## 架构设计

基于 **Tokenizer-Free + Diffusion Autoregressive** 范式，模型完全在 AudioVAE V2 的潜空间中运行，四阶段管线：**LocEnc → TSLM → RALM → LocDiT**。

## 安装与使用

```bash
# 安装
pip install voxcpm

# 要求：Python ≥ 3.10, PyTorch ≥ 2.5.0, CUDA ≥ 12.0
```

```python
from voxcpm import VoxCPM
import soundfile as sf

model = VoxCPM.from_pretrained("openbmb/VoxCPM2", load_denoiser=False)

# 基础 TTS
wav = model.generate(
    text="Hello, welcome to VoxCPM2!",
    cfg_value=2.0,
    inference_timesteps=10,
)
sf.write("demo.wav", wav, model.tts_model.sample_rate)

# Voice Design（自然语言描述创建声音）
wav = model.generate(
    text="(A young woman, gentle and sweet voice)Hello, welcome!",
    cfg_value=2.0, inference_timesteps=10,
)

# 可控语音克隆
wav = model.generate(
    text="(slightly faster, cheerful tone)This is a cloned voice.",
    reference_wav_path="path/to/voice.wav",
    cfg_value=2.0, inference_timesteps=10,
)

# 流式输出
for chunk in model.generate_streaming(text="Streaming TTS is easy!"):
    # 实时处理音频块
    pass
```

CLI 使用：

```bash
# Voice Design
voxcpm design --text "Your text here." --output out.wav

# 语音克隆
voxcpm clone --text "Cloned speech." --reference-audio ref.wav --output out.wav

# 终极克隆
voxcpm clone --text "Text" --prompt-audio ref.wav --prompt-text "transcript" --output out.wav
```

## 微调

支持全量微调（SFT）和 LoRA 微调，仅需 5-10 分钟音频即可适配特定说话人、语言或领域：

```bash
# LoRA 微调（推荐）
python scripts/train_voxcpm_finetune.py \
    --config_path conf/voxcpm_v2/voxcpm_finetune_lora.yaml

# WebUI 微调界面
python lora_ft_webui.py
```

## 生产部署

| 方案 | 特点 | RTF (4090) |
|------|------|:---:|
| 标准 PyTorch | 开箱即用 | ~0.30 |
| [Nano-vLLM](https://github.com/a710128/nanovllm-voxcpm) | 高吞吐并发推理 | ~0.13 |
| [vLLM-Omni](https://github.com/vllm-project/vllm-omni) | OpenAI 兼容 API、PagedAttention、多 GPU | — |
| [VoxCPM.cpp](https://github.com/bluryar/VoxCPM.cpp) | CPU/CUDA/Vulkan 推理 | — |
| [VoxCPM-ONNX](https://github.com/bluryar/VoxCPM-ONNX) | ONNX CPU 推理 | — |
| [VoxCPMANE](https://github.com/0seba/VoxCPMANE) | Apple Neural Engine | — |

## 亮点 / 个人评价

- **Tokenizer-Free 创新**：绕过语音离散化，直接在连续潜空间生成，从根本上避免了信息损失
- **Voice Design 独特能力**：仅凭文字描述就能创造全新声音，这在开源 TTS 中非常少见
- **性能强劲**：在 Seed-TTS-eval、CV3-eval 等公开基准上达到 SOTA 或可比水平，语音相似度（SIM）指标尤其突出
- **生态丰富**：vLLM 集成、ComfyUI 节点、ONNX/CPP 推理、Apple ANE 适配，覆盖从研究到生产的完整链路
- **中文支持优秀**：支持普通话及四川话、粤语、吴语、东北话等多种方言
