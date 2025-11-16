# Contributing to Cybersecurity-Portfolio

Thank you for your interest in contributing to this cybersecurity portfolio! This document provides guidelines for collaboration, feedback, and contributions.

---

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How to Contribute](#how-to-contribute)
- [Reporting Issues](#reporting-issues)
- [Suggesting Enhancements](#suggesting-enhancements)
- [Pull Request Process](#pull-request-process)
- [Style Guidelines](#style-guidelines)
- [Community & Support](#community--support)

---

## 🤝 Code of Conduct

### Our Commitment

We are committed to providing a welcoming and inclusive environment for all contributors. We expect all participants to:

- ✅ Treat each other with respect and professionalism
- ✅ Welcome diverse perspectives and backgrounds
- ✅ Focus on constructive feedback and collaboration
- ✅ Report inappropriate behavior to the repository maintainers

### Unacceptable Behavior

The following are not tolerated:
- ❌ Harassment, discrimination, or hateful comments
- ❌ Threats or intimidation
- ❌ Posting of private information without consent
- ❌ Other conduct that violates professional standards

---

## 🚀 How to Contribute

### Types of Contributions We Welcome

1. **Bug Reports** – Found an issue? Let us know!
2. **Documentation Improvements** – Better explanations, examples, or corrections
3. **New Project Examples** – Additional security labs or projects
4. **Code Reviews** – Feedback on existing content
5. **Cheat Sheet Enhancements** – Additional resources or clarifications
6. **Tool Recommendations** – Suggestions for new security tools or techniques

### Getting Started

1. **Fork the Repository**
   ```bash
   git clone https://github.com/michael-cybersec/Cybersecurity-Portfolio.git
   cd Cybersecurity-Portfolio
   ```

2. **Create a Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make Your Changes**
   - Edit files, add new content, or improve documentation
   - Keep changes focused and atomic

4. **Commit Your Work**
   ```bash
   git commit -m "Add descriptive commit message"
   ```

5. **Push to Your Fork**
   ```bash
   git push origin feature/your-feature-name
   ```

6. **Submit a Pull Request**
   - Provide a clear description of your changes
   - Reference any related issues

---

## 🐛 Reporting Issues

### Before Submitting a Bug Report

- Check if the issue has already been reported
- Verify you're using the latest version of the portfolio
- Gather relevant context (OS, tool versions, error messages)

### How to Submit a Bug Report

Use GitHub Issues with the following template:

```markdown
**Description:**
Clear description of the bug

**Steps to Reproduce:**
1. Step one
2. Step two
3. Step three

**Expected Behavior:**
What should happen

**Actual Behavior:**
What actually happened

**Environment:**
- OS: [e.g., Windows 10, Ubuntu 20.04]
- Tools: [e.g., Splunk, Metasploit versions]
- Browser: [if applicable]

**Additional Context:**
Screenshots, logs, or other relevant information
```

---

## 💡 Suggesting Enhancements

We love ideas! Here's how to suggest an enhancement:

### Enhancement Proposal Template

```markdown
**Title:** Brief description of enhancement

**Problem Statement:**
What problem does this solve?

**Proposed Solution:**
How would this enhancement work?

**Alternative Solutions:**
Any other approaches considered?

**Additional Context:**
References, examples, or related work
```

### Examples of Good Enhancement Ideas

- ✅ New security project example with detailed walkthrough
- ✅ Expanded cheat sheet for a specific domain
- ✅ Improved documentation or formatting
- ✅ Links to valuable external resources
- ✅ New lab scenarios or challenges

---

## 📝 Pull Request Process

### Requirements for Pull Requests

1. **Update Documentation**
   - Ensure any new content includes proper documentation
   - Update the main README if adding new sections

2. **Follow Style Guidelines**
   - See [Style Guidelines](#style-guidelines) below
   - Use markdown formatting consistently

3. **Test Your Changes**
   - Verify all links work correctly
   - Check markdown rendering (especially code blocks)
   - Ensure no confidential information is included

4. **Write Clear Commit Messages**
   - Use present tense: "Add feature" not "Added feature"
   - Be specific: "Add SIEM correlation rules guide" not "Update docs"

5. **Reference Issues**
   - If fixing an issue: "Fixes #123"
   - If related to an issue: "Related to #456"

### PR Review Process

- Maintainer(s) will review your PR
- Constructive feedback may be provided
- Changes may be requested before merging
- Once approved, your PR will be merged

### After Merge

- Your contributions will be credited
- Changes will be published to the live repository
- Thank you for improving the portfolio!

---

## 🎨 Style Guidelines

### Markdown Formatting

**Headings:**
```markdown
# H1 – Main title
## H2 – Major sections
### H3 – Subsections
#### H4 – Details
```

**Lists & Formatting:**
```markdown
- Bullet point
- Another bullet

1. Numbered item
2. Another item

**Bold text** for emphasis
*Italic text* for alternatives
`code snippet` for inline code
```

**Code Blocks:**
````markdown
```bash
command-line example
```

```python
# Python code example
def example():
    pass
```
````

### Project Documentation

Each project README should include:
- Clear title and description
- Environment/tools used
- Step-by-step process
- Key findings or results
- Artifacts and links
- How to reproduce (where applicable)

### Naming Conventions

- **Branches:** `feature/description` or `fix/description`
- **Files:** Use hyphens for readability: `security-tools.md`
- **Commits:** Start with verb: "Add", "Fix", "Update", "Improve"

### Security Best Practices

⚠️ **Never commit:**
- API keys or credentials
- Private SSH keys
- Passwords or sensitive data
- Personal identifying information

✅ **Always use:**
- Environment variables for secrets
- `.gitignore` to exclude sensitive files
- Placeholder text for examples

---

## 📚 Documentation Standards

### For New Projects

Include:
- **Title** – Clear, descriptive name
- **Objective** – What the project demonstrates
- **Tools & Technologies** – What was used
- **Process** – Step-by-step walkthrough
- **Findings** – Key results and insights
- **Lessons Learned** – What you took away
- **Artifacts** – Links to reports, code, diagrams

### For Cheat Sheets

Include:
- **Topic** – Clear subject matter
- **Quick Reference** – Fast lookup format
- **Common Commands** – Practical examples
- **Tips & Tricks** – Pro tips
- **Resources** – Links for deeper learning

### For Write-ups

Include:
- **Challenge/Lab Name** – Specific reference
- **Difficulty Level** – Easy, Medium, Hard
- **Summary** – Brief overview
- **Walkthrough** – Detailed steps
- **Key Concepts** – What you learned
- **Tools Used** – Specific applications
- **Flags/Solutions** – Final answers (if applicable)

---

## 🤖 Automation & Quality Checks

This repository uses:
- **Git** – Version control and history
- **Markdown Linting** – Optional: consistency checks
- **Security Scanning** – Automated secret detection

Before submitting PRs, ensure:
- No broken links
- Proper markdown syntax
- No accidental credential commits

---

## 💬 Community & Support

### Getting Help

- **General Questions:** Open a GitHub Discussion
- **Bug Reports:** Open a GitHub Issue
- **Feature Requests:** Use the Discussions tab
- **Direct Contact:** See main README for email

### Communication Channels

- GitHub Issues – Bug reports and feature requests
- GitHub Discussions – Questions and ideas
- Pull Requests – Code and documentation changes

### Recognition

Contributors will be recognized:
- In commit history
- In project README (with permission)
- Through GitHub's contributor graph

---

## 📖 Additional Resources

- [GitHub Guides](https://guides.github.com/)
- [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
- [OWASP Security Guidelines](https://owasp.org/)
- [SANS Security Resources](https://www.sans.org/)

---

## 📄 License

By contributing to this repository, you agree that your contributions will be licensed under the MIT License (see LICENSE file).

---

## 🙏 Thank You

We appreciate your interest in contributing! Your feedback, improvements, and ideas help make this portfolio better for everyone.

**Happy contributing! 🛡️**

---

*Last Updated: November 2025*  
*Maintained by: Michael Taylor (michael-cybersec)*
