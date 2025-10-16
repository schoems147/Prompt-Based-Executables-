# Prompt-Based Executables (PBE)

**Make AI interactions portable, reproducible, and shareable.**

A Prompt-Based Executable (PBE) is a JSON file that configures AI behavior. Load it into any compatible LLM, and the AI immediately adopts the defined behavior, structure, and personality—no coding required.

---

## 🎯 What Problem Does This Solve?

**The Problem:**
- Every time you use an AI, you start from scratch
- That perfect prompt you crafted yesterday? You have to remember it or dig through chat history
- Want to share your workflow with a teammate? Copy-paste doesn't capture the full context
- Switch from Claude to ChatGPT? Your carefully-tuned interaction style doesn't transfer

**The Solution:**
PBEs are **reusable behavior templates** for AI. Create once, use everywhere, share with anyone.

---

## ⚡ Quick Start

### 1. Choose a PBE
Browse the [`/pbes/`](/pbes/) directory and pick one that interests you. For example: [`simple_quiz.pbe.txt`](/pbes/interactive_engine/simple_quiz.pbe.txt)

### 2. Copy the entire file content

### 3. Paste it into your LLM
Works with:
- Claude (Anthropic)
- ChatGPT (OpenAI)
- Gemini (Google)
- Other instruction-following LLMs

### 4. The AI immediately executes
No installation. No setup. No API keys. Just paste and go.

---

## 💡 What Can You Build?

### Interactive Engines
- Educational tutors and quiz systems
- Text-based games and adventures
- Brainstorming and ideation facilitators
- Decision-making frameworks
- Creative writing partners

### Stateless Executors
- Code reviewers and analyzers
- Document summarizers
- Data formatters
- Translation tools
- Content generators

### Persistent Services *(Coming Soon)*
- Background monitors
- Scheduled assistants
- Event-driven automation

---

## 🏗️ How It Works

A PBE is structured JSON with three core components:

```json
{
  "pbe_name": "unique_identifier",
  "pbe_version": "1.0.0",
  "pbe_class": "interactive_engine",
  "install_instructions": "This is a Prompt-Based Executable...",
  
  "description": "What this PBE does",
  "core_philosophy": { ... },
  "game_structure": { ... },
  "facilitator_techniques": { ... }
}
```

The LLM reads this structure and adopts the defined behavior. It's like loading a cartridge into a game console—same console, different game.

**[Read the full specification →](SPECIFICATION.md)**

---

## 🌟 Example: The What-If Game

The PBE that started it all. A text-based game that teaches improvisational systems thinking through creative problem-solving scenarios.

**Load it:** [`what_if_game.pbe.txt`](/pbes/interactive_engine/what_if_game.pbe.txt)

**Try it:** Paste into any LLM and start playing immediately.

**Learn from it:** See how interactive engines structure multi-phase experiences.

---

## 🤝 Contributing

We welcome contributions! Whether you're:
- **Creating new PBEs** for the community
- **Improving documentation**
- **Testing cross-platform compatibility**
- **Sharing use cases and examples**

**[Read the contributing guide →](CONTRIBUTING.md)**

### Quality Standards
- Must follow the [PBE Specification](SPECIFICATION.md)
- Must be tested on at least 2 LLM platforms
- Must include clear description and use case
- Interactive engines need 5+ facilitator techniques

---

## 📖 Learn More

- **[Getting Started Guide](docs/getting_started.md)** - Deep dive into using and creating PBEs
- **[Design Philosophy](docs/design_philosophy.md)** - Why PBEs exist and design principles
- **[FAQ](docs/faq.md)** - Common questions answered
- **[Roadmap](ROADMAP.md)** - Where this is heading

---

## 🎨 Use Cases

**Education:**
- Custom tutoring systems for any subject
- Interactive learning games
- Assessment and quiz tools

**Productivity:**
- Structured brainstorming sessions
- Decision-making frameworks
- Meeting facilitators

**Creative:**
- Writing workshops
- Character development tools
- Story generators

**Development:**
- Code review assistants
- Documentation generators
- API testing helpers

**[See detailed examples →](examples/use_cases.md)**

---

## 🔧 Tools

**[PBE Creator Tool (PBCT)](tools/pbct.pbe.txt)**
An interactive PBE that helps you create new PBEs through guided dialogue. Meta? Yes. Useful? Absolutely.

---

## 🚀 The Vision

PBEs are the first step toward an **AI Operating System**—a framework where AI behaviors are:
- **Portable** across platforms
- **Composable** into larger systems
- **Trustworthy** by design
- **Open** for everyone

This is infrastructure for human-AI coexistence that prioritizes user wellbeing over corporate interests.

---

## 📊 Current Status

- **Specification:** v1.0 (Stable)
- **PBE Classes:** 2 of 3 implemented (stateless_executor, interactive_engine)
- **Platform Compatibility:** Claude, ChatGPT, Gemini (tested)
- **Community:** Just getting started—be an early contributor!

---

## 🙏 About

The PBE standard was created by a systems thinker who happened to be working in manual labor. Built entirely on a mobile phone over one week using nothing but LLM interactions and determination.

Proof that you don't need a computer science degree or fancy tools to build foundational infrastructure—you need systematic thinking and real problems to solve.

**[Read the full story →](AUTHOR.md)**

---

## 📜 License

MIT License - Use freely, commercially or personally, with attribution.

See [LICENSE](LICENSE) for details.

---

## 🌐 Connect

- **Issues:** Report bugs or request features
- **Discussions:** Share ideas and use cases
- **Pull Requests:** Contribute PBEs or improvements

**Let's build the future of AI interaction together.**

---

## Star History

If you find PBEs useful, give us a star ⭐ to help others discover the project!

---

*"Technology should improve quality of life, not extract from it."*