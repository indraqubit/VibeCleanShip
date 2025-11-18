# Contributing to Vibe Coding Methodology

Thank you for your interest in contributing to the **Vibe Coding Methodology**! This document provides guidelines for how to contribute to this project and ensure a smooth collaboration experience.

## 🎯 How to Contribute

### Ways to Contribute

#### 1. **Improve Documentation**
- Add examples or clarify explanations
- Translate documentation to other languages
- Create video tutorials or screencasts
- Add diagrams or visual aids

#### 2. **Share Experience**
- Submit success/failure stories from using vibe coding
- Document lessons learned
- Add case studies with metrics (time saved, complexity managed)

#### 3. **Stack Extensions**
- Add support for new technology stacks (Flutter, Go, etc.)
- Document tool-specific workflows
- Create stack-specific cleanup checklists

#### 4. **Tool Integration**
- Scripts and automations for existing tools
- New AI tool integration guides
- Framework improvements

#### 5. **Code Contribution**
- Framework improvements (`vibe-coding-framework.js`)
- Documentation tooling
- Testing automation

### 🐛 Reporting Issues

When reporting bugs or requesting features:

1. **Check Existing Issues** - Search [GitHub Issues](https://github.com/indraqubit/VibeCleanShip/issues) first
2. **Use Issue Templates** - Choose the appropriate template when available
3. **Provide Context** - Include tech stack, methodology phase, and expected vs actual behavior
4. **Attach Examples** - Code snippets, error messages, timing data

### 🛠️ Development Process

#### For Code Contributions

1. **Fork the Repository**
   ```bash
   git clone https://github.com/indraqubit/VibeCleanShip.git
   cd VibeCleanShip
   git checkout -b feature/your-feature-name
   ```

2. **Follow Methodology Yourself**
   - Use vibe coding to implement your changes
   - Document your process for others to learn

3. **Test Your Changes**
   ```bash
   npm test
   # Or run framework directly
   node vibe-coding-framework.js
   ```

4. **Follow Code Standards**
   - Use clear, descriptive commit messages with `vibe:` prefix during development
   - Update documentation for any functional changes
   - Ensure all examples still work

#### For Documentation Contributions

1. **Follow Structure** - Use existing patterns (sections, formatting, linking)
2. **Add Examples** - Include concrete code snippets and workflow examples
3. **Cross-Reference** - Link related sections and alternative approaches
4. **Keep Updated** - Update references when changing section titles

### 📝 Commit Guidelines

We follow a variant of [Conventional Commits](https://conventionalcommits.org/):

#### Examples

```bash
# Vibe coding commits (during implementation)
vibe: add React TypeScript workflow examples
vibe: implement basic session tracking in framework

# Cleanup commits (when polishing)
refactor: extract validation helpers from main classes
docs: clarify Post-Vibe Workflow phases

# Final commits (production-ready)
feat: add Rust + Tokio stack support
fix: correct Mermaid diagram in README
docs: add Japanese translation of philosophy
```

#### Message Structure
```
type(scope): description

[optional body]

[optional footer]
```

Where `type` is one of:
- `vibe` - Rapid development work
- `feat` - New features (post-cleanup)
- `fix` - Bug fixes
- `docs` - Documentation
- `refactor` - Code restructuring
- `style` - Code style changes
- `test` - Testing
- `chore` - Maintenance

### 🎯 Guidelines

#### Content Guidelines
- **Be Practical** - Include time estimates, failure stories, and trade-offs
- **Focus on Results** - Share what worked, what didn't, and why
- **Stay Beginner-Friendly** - Assume varying experience levels
- **Celebrate Balance** - Show how vibes and discipline combine for results

#### Code Quality
- **Test Methodology** - Validate that your suggestions actually work
- **Document Trade-offs** - What's fast vs what's maintainable
- **Include Benchmarks** - Time saved, complexity managed, etc.
- **Future-Proof** - Consider how this scales in larger projects

#### Review Process
All contributions undergo review to ensure:

- **Methodology Alignment** - Follows core vibe coding principles
- **Practical Value** - Provides real benefit to practitioners
- **Clarity** - Clear explanations and examples
- **Accuracy** - Technically correct information

### 🤝 Getting Help

- **Questions**: [GitHub Discussions](https://github.com/indraqubit/VibeCleanShip/discussions)
- **Issues**: Descriptive bug reports and feature requests
- **Reviews**: Constructive feedback appreciated
- **Collaboration**: See [Sparring Partner Concept](./SPARRING_PARTNER.md) for effective partnership in vibe coding

### 📜 Code of Conduct

This project follows our [Code of Conduct](./CODE_OF_CONDUCT.md). By participating, you agree to:
- Be respectful and inclusive
- Focus on constructive feedback
- Value diverse perspectives
- Maintain professional discourse

### 📊 Recognition

Contributors are recognized in:
- CHANGELOG.md for significant contributions
- README.md contributors section
- Future acknowledgments as the methodology evolves

---

**Ready to contribute? See the [Quick Start](./README.md#quick-start) guide to get familiar with the methodology, then create your first `vibe:` commit!** 🚀
