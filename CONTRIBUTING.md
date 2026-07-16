# Contributing to STCO Simulator

Thank you for your interest in contributing to the STCO Simulator! This guide will help you get started.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How to Contribute](#how-to-contribute)
- [Development Setup](#development-setup)
- [Contribution Guidelines](#contribution-guidelines)
- [Hardware Presets](#adding-hardware-presets)
- [Lab Exercises](#adding-lab-exercises)
- [Pull Request Process](#pull-request-process)

## Code of Conduct

This project is dedicated to providing a welcoming and inclusive experience for everyone. Please be respectful and constructive in all interactions.

## How to Contribute

### 🐛 Reporting Bugs

1. Check [existing issues](https://github.com/kvbulusu/ai-silicon-simulator/issues) to avoid duplicates
2. Open a new issue with:
   - Browser and OS information
   - Steps to reproduce
   - Expected vs actual behavior
   - Screenshots if applicable

### 💡 Suggesting Features

1. Open an issue with the `enhancement` label
2. Describe the feature and its value to users
3. Reference relevant book chapters if applicable

### 🔧 Code Contributions

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/my-feature`)
3. Make your changes
4. Test thoroughly (desktop + mobile)
5. Submit a pull request

## Development Setup

The simulator is a single HTML file with no build step required:

```bash
# Clone the repository
git clone https://github.com/kvbulusu/ai-silicon-simulator.git
cd ai-silicon-simulator

# Open in browser
open index.html
# or
python3 -m http.server 8080
```

### Dependencies (CDN-loaded)

- **Tailwind CSS** — Utility classes
- **Chart.js** — Break-even visualization
- **html2canvas** — Screenshot export
- **Google Fonts** — Space Grotesk, JetBrains Mono

## Contribution Guidelines

### Adding Hardware Presets

Hardware presets are defined in the `HW_DB` object. To add a new preset:

```javascript
"your-chip-id": {
    "name": "Chip Name",
    "node": "5nm",           // Process node
    "pkg": "2.5d",           // monolithic | 2.5d | 3d
    "freq": 1800,            // MHz
    "tdp": 700,              // Watts
    "memType": "hbm3e",      // hbm4 | hbm3e | hbm3 | hbm2e | lpddr5 | ddr5
    "memBW": 4800,           // GB/s
    "memCap": 128,           // GB
    "cores": 16384,          // CUDA cores or equivalent
    "interconnect": "nvlink5", // nvlink5 | nvlink4 | ualink | pcie6 | pcie5
    "precision": "fp8",      // fp32 | fp16 | fp8 | fp4 | int8 | int4
    "cooling": "liquid",     // liquid | air | passive
    "category": "datacenter", // datacenter | edge | aipc
    "year": 2025,
    "costEst": 30000         // USD estimated cost
}
```

**Requirements:**
- All values must come from official datasheets or reliable sources
- Include a link to the datasheet in your PR description
- Add the preset to the `<select>` element in the HTML

### Adding Lab Exercises

Lab exercises follow this structure:

```html
<div class="exercise-card">
    <h4>Exercise X.Y: Title</h4>
    <p><strong>Scenario:</strong> Context for the exercise</p>
    <p><strong>Task:</strong></p>
    <ol>
        <li>Step 1</li>
        <li>Step 2</li>
    </ol>
    <button onclick="toggleSolution('ex-X-Y')" class="reveal-btn">💡 Show Solution</button>
    <div id="ex-X-Y" class="solution" style="display:none;">
        <h5>Solution:</h5>
        <!-- Solution content -->
        <p><strong>Key Insight:</strong> What the student should learn</p>
    </div>
</div>
```

**Requirements:**
- Reference specific book chapters
- Include a "Key Insight" that connects to broader concepts
- Provide concrete numbers, not just qualitative answers
- Test that any "Load Configuration" buttons work correctly

### Code Style

- Use semantic HTML where possible
- Keep CSS compact (the file uses abbreviated class names for size)
- JavaScript: use `const`/`let`, template literals, arrow functions
- Test on Chrome, Firefox, and Safari
- Test on mobile (or use Chrome DevTools mobile emulation)

## Pull Request Process

1. **Title**: Use conventional commit format (e.g., `feat: add MI400X preset`)
2. **Description**: Explain what and why, reference issues
3. **Testing**: Confirm testing on desktop + mobile
4. **Attribution**: If adding hardware data, cite the source

### PR Review Criteria

- [ ] Code works correctly (no console errors)
- [ ] Mobile responsive (tested at 375px width)
- [ ] Dark/light mode compatible
- [ ] Book chapter references are accurate
- [ ] Hardware specs match official datasheets

## 📜 License

By contributing, you agree that your contributions will be licensed under the [CC BY-NC-SA 4.0](LICENSE.md) license.

## Questions?

- Open an [issue](https://github.com/kvbulusu/ai-silicon-simulator/issues) for questions
- Tag [@kbulusu](https://twitter.com/kbulusu) on Twitter/X

---

Thank you for helping make the STCO Simulator better! 🙏
