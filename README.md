# 🔬 STCO Simulator v2

**Silicon-Thermal-Software Co-Optimization Simulator — 2026 Edition**

Interactive tool for analyzing AI hardware performance, economics, and bottlenecks.

[![Live Demo](https://img.shields.io/badge/demo-live-brightgreen)](https://kvbulusu.github.io/ai-silicon-simulator/)
[![License](https://img.shields.io/badge/license-CC%20BY--NC--SA%204.0-blue)](LICENSE.md)
[![Book](https://img.shields.io/badge/book-Bridging%20AI%20and%20Silicon-purple)](#-about)

## 📚 About

This simulator is the interactive companion tool for the book:

**"Bridging AI and Silicon: A Practitioner's Guide"**
by Kiran Bulusu (24 years semiconductor experience)

The simulator brings to life the frameworks, calculations, and tradeoffs discussed in Chapters 8–16, allowing you to experiment with hardware configurations, workload types, and economic scenarios.

## ✨ Features

### 🖥️ Hardware Coverage (2024–2026)
- **NVIDIA**: A100, H100, H200 (HBM3e), B100/B200 (Blackwell, FP4 support)
- **AMD**: MI300X, MI350
- **Intel**: Gaudi 3
- **Edge AI**: Jetson Orin NX, Jetson AGX Orin, Cloud AI 100, Edge TPU
- **AI PC/NPU**: Intel Core Ultra, AMD Ryzen AI, Snapdragon X Elite, Apple M4

### 📊 Analysis Capabilities
- **Roofline Model**: Identify compute vs memory vs network bottlenecks
- **TCO Calculator**: 3-year total cost of ownership with cloud comparison
- **Power Iceberg**: Chip → Server → Rack → Datacenter power cascade
- **Agentic AI Economics**: Multi-step workflow GPU utilization modeling
- **Build vs Buy**: Custom silicon NRE break-even analysis
- **Cloud vs On-Prem**: Interactive break-even visualizer

### 🎓 Educational Features
- **Progressive Lab Exercises**: 7 hands-on problems across 5 chapters with solutions
- **Interactive Visualizations**: Roofline model, silicon thermal diagrams
- **CODF Framework**: Integrated optimization decision tree
- **Book Scenarios**: Pre-configured case studies from the book
- **Tooltip Help System**: Contextual explanations for every parameter

### 🚀 Advanced Features
- **Comparison Mode**: Side-by-side hardware analysis (up to 3 configs)
- **Export Configs**: JSON, Python script, shareable URLs
- **Dark/Light Mode**: Toggle for eye-friendly interface
- **Mobile Responsive**: Works on all devices with touch-friendly controls
- **Social Sharing**: Share configurations on Twitter/X, LinkedIn, Reddit
- **Screenshot Export**: Full-page capture for presentations

## 🎯 Use Cases

### For Students & Educators
- Learn AI hardware tradeoffs hands-on
- Visualize concepts from the book (Chapters 8–16)
- Complete chapter exercises interactively with built-in solutions

### For Practitioners & Engineers
- Size hardware for your specific workload
- Compare build vs buy economics for custom silicon
- Identify performance bottlenecks using the Roofline Model
- Validate architecture decisions before procurement

### For Executives & Product Managers
- Understand TCO and break-even volumes
- Compare cloud vs on-premise costs over 3 years
- Make data-driven hardware investment decisions

## 🚀 Quick Start

1. **Try it live**: [kvbulusu.github.io/ai-silicon-simulator](https://kvbulusu.github.io/ai-silicon-simulator/)
2. **Select a hardware preset**: H100, B200, MI300X, or any of 20+ options
3. **Choose a workload**: Inference Decode, Agentic AI, Training, Edge, AI PC
4. **Analyze results**: Check bottlenecks, costs, and optimization recommendations
5. **Try Lab Exercises**: Work through guided problems with solutions

## 📖 Book Scenarios

Pre-configured scenarios from the book:

| Scenario | Chapter | What You Learn |
|----------|---------|----------------|
| H100 Cluster Power Analysis | Ch. 8 | Power draw, thermal behavior |
| DVFS Power-Performance Tradeoff | Ch. 8 | Cubic power law, efficiency curves |
| HBM3 vs HBM3e vs HBM4 | Ch. 10 | Memory bandwidth impact |
| Memory vs Compute Bottleneck | Ch. 11 | Roofline model interpretation |
| Agentic vs Traditional Inference | Ch. 14 | GPU utilization economics |
| Custom Silicon Build vs Buy | Ch. 16 | NRE amortization, break-even |

## 🤝 Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Ways to contribute:**
- 🐛 Report bugs or suggest features via [Issues](https://github.com/kvbulusu/ai-silicon-simulator/issues)
- 📝 Improve documentation
- 🧪 Add new hardware presets (with datasheet references)
- 🎓 Create new lab exercises
- 🌍 Add translations

## 📜 License

This project is licensed under **CC BY-NC-SA 4.0** (Creative Commons Attribution-NonCommercial-ShareAlike 4.0).

**TL;DR:**
- ✅ Use for education, research, personal projects
- ✅ Modify and share (with attribution)
- ❌ Commercial use requires separate license

See [LICENSE.md](LICENSE.md) for full terms.

## 🙏 Citation

If you use this simulator in your research or teaching, please cite:

```bibtex
@misc{bulusu2026stco,
  author = {Bulusu, Kiran},
  title = {STCO Simulator: Silicon-Thermal-Software Co-Optimization Tool},
  year = {2026},
  publisher = {GitHub},
  url = {https://github.com/kvbulusu/ai-silicon-simulator}
}
```

## 📞 Contact

- **Author**: Kiran Bulusu
- **Twitter/X**: [@kbulusu](https://twitter.com/kbulusu)
- **Issues**: [GitHub Issues](https://github.com/kvbulusu/ai-silicon-simulator/issues)

## 🌟 Star This Repo

If you find this simulator useful, please ⭐ star it on GitHub!

Every star helps more people discover this educational tool.

---

**Built with ❤️ for the AI hardware community**

*"Understanding the silicon beneath the intelligence"*
