# 🛡️ APort - Agent Identity & Policy Enforcement

<div align="center">

![APort Logo](https://img.shields.io/badge/APort-Agent%20Passport-blue?style=for-the-badge&logo=shield&logoColor=white)

**The neutral, portable passport + verify + suspend rail for AI agents**

[![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-Ready-green?style=flat-square&logo=github-actions)](https://github.com/aporthq/policy-verify-action)
[![API Status](https://img.shields.io/badge/API-Live-brightgreen?style=flat-square&logo=api)](https://api.aport.io)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)
[![Discord](https://img.shields.io/badge/Discord-Join-blue?style=flat-square&logo=discord)](https://discord.gg/aport)

[🌐 Website](https://aport.io) • [📚 Docs](https://aport.io/docs) • [🚀 Try Now](https://aport.io/dashboard) • [💬 Community](https://discord.gg/aport)

</div>

---

## 🎯 The Problem

<div align="center">

```mermaid
graph TD
    A[🤖 AI Agent] --> B[💳 Refund $1000]
    A --> C[📊 Export 1M Rows]
    A --> D[🔀 Merge to Main]
    A --> E[🚀 Deploy to Prod]
    
    B --> F[❌ No Identity Check]
    C --> F
    D --> F
    E --> F
    
    F --> G[💥 Security Incident]
    G --> H[⏰ Hours to Detect]
    H --> I[💰 $10K+ in Damages]
    
    style A fill:#ff6b6b
    style F fill:#ff6b6b
    style G fill:#ff6b6b
    style I fill:#ff6b6b
```

**Organizations are letting AI agents perform sensitive actions without proper identity verification or policy enforcement.**

</div>

## ✨ The Solution

<div align="center">

```mermaid
graph TD
    A[🤖 AI Agent] --> B[🛡️ APort Verify]
    B --> C{Policy Check}
    C -->|✅ Allowed| D[✅ Action Proceeds]
    C -->|❌ Blocked| E[🚫 Action Blocked]
    
    F[👤 Agent Passport] --> B
    G[📋 Policy Pack] --> B
    H[⚡ Global Suspend] --> B
    
    style A fill:#4ecdc4
    style B fill:#45b7d1
    style D fill:#96ceb4
    style E fill:#feca57
    style F fill:#ff9ff3
    style G fill:#ff9ff3
    style H fill:#ff9ff3
```

**APort provides a neutral, portable identity and policy enforcement layer for AI agents across all platforms.**

</div>

## 🚀 Quick Start

### 1. Create Your Agent Passport

```bash
# Install APort CLI
npm install -g @aport/cli

# Create a new agent
aport create-agent --name "My AI Assistant" --role "Customer Support"
```

### 2. Add Policy Enforcement

```yaml
# .github/workflows/aport-check.yml
name: APort Policy Check
on: [pull_request]

jobs:
  policy-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: aporthq/policy-verify-action@v1
        with:
          agent-id: ${{ secrets.APORT_AGENT_ID }}
```

### 3. Integrate with Your App

```javascript
// Node.js Integration
import { verifyPolicy } from '@aport/sdk';

const result = await verifyPolicy({
  agentId: 'agt_123',
  policyPack: 'refunds.v1',
  context: {
    amount: 100,
    currency: 'USD',
    customerId: 'cust_456'
  }
});

if (!result.allowed) {
  throw new Error(`Action blocked: ${result.reason}`);
}
```

## 🎨 Features

<div align="center">

| 🏷️ **Feature** | 📝 **Description** | 🎯 **Use Case** |
|---|---|---|
| **🆔 Agent Identity** | Portable passports with capabilities & limits | Know who your agents are |
| **📋 Policy Packs** | Pre-built policies for common actions | Enforce business rules |
| **⚡ Real-time Verify** | Sub-100ms policy checks | Block bad actions instantly |
| **🚨 Global Suspend** | Kill switch across all platforms | Stop incidents in seconds |
| **🔐 Multi-level Assurance** | Email, GitHub, Domain verification | Trust but verify |
| **📊 Audit Trail** | Complete action history | Compliance & debugging |

</div>

## 🛠️ Supported Platforms

<div align="center">

```mermaid
graph LR
    A[🛡️ APort Core] --> B[💳 Payments]
    A --> C[📊 Data Export]
    A --> D[🔀 Git Operations]
    A --> E[🚀 CI/CD]
    A --> F[💬 Messaging]
    
    B --> B1[Stripe<br/>PayPal<br/>Square]
    C --> C1[Segment<br/>Fivetran<br/>Snowflake]
    D --> D1[GitHub<br/>GitLab<br/>Bitbucket]
    E --> E1[GitHub Actions<br/>Jenkins<br/>CircleCI]
    F --> F1[Slack<br/>Discord<br/>Teams]
    
    style A fill:#45b7d1
    style B fill:#96ceb4
    style C fill:#feca57
    style D fill:#ff9ff3
    style E fill:#ff6b6b
    style F fill:#4ecdc4
```

</div>

## 📦 Policy Packs

### 💳 Refunds Protection
```json
{
  "policy": "refunds.v1",
  "limits": {
    "max_refund_per_tx": 1000,
    "max_refunds_per_day": 10,
    "allowed_currencies": ["USD", "EUR"]
  }
}
```

### 📊 Data Export Control
```json
{
  "policy": "data_export.v1", 
  "limits": {
    "max_rows_per_export": 100000,
    "allow_pii": false,
    "allowed_datasets": ["users", "orders"]
  }
}
```

### 🔀 Repository Safety
```json
{
  "policy": "repo.v1",
  "limits": {
    "max_prs_per_day": 5,
    "allowed_repos": ["owner/repo1"],
    "require_review": true
  }
}
```

## 🎯 Real-World Examples

### 🛒 E-commerce Refund Bot
```javascript
// Before APort
const refund = await stripe.refunds.create({
  amount: 50000, // $500 - no checks!
  payment_intent: paymentIntentId
});

// After APort
const policyCheck = await verifyPolicy({
  agentId: 'refund-bot-001',
  policyPack: 'refunds.v1',
  context: { amount: 50000, currency: 'USD' }
});

if (policyCheck.allowed) {
  const refund = await stripe.refunds.create({
    amount: 50000,
    payment_intent: paymentIntentId
  });
}
```

### 🔀 GitHub PR Automation
```yaml
# .github/workflows/auto-merge.yml
name: Auto Merge
on:
  pull_request:
    types: [opened, synchronize]

jobs:
  check-and-merge:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: aporthq/policy-verify-action@v1
        with:
          agent-id: ${{ secrets.APORT_AGENT_ID }}
          policy-pack: 'repo.v1'
      - name: Auto Merge
        if: success()
        run: gh pr merge --auto
```

## 📊 Performance & Reliability

<div align="center">

| **Metric** | **Target** | **Actual** |
|---|---|---|
| **⚡ Verify Latency** | <100ms p95 | **~50ms p95** |
| **🚨 Suspend Time** | <30s global | **~15s global** |
| **📈 Uptime** | 99.9% | **99.99%** |
| **🔄 Throughput** | 10k req/s | **50k+ req/s** |

</div>

## 🏆 Why Choose APort?

<div align="center">

```mermaid
graph TD
    A[🤔 Current State] --> B[❌ Custom Solutions]
    A --> C[❌ Platform Lock-in]
    A --> D[❌ No Global Control]
    
    E[✨ With APort] --> F[✅ Standardized]
    E --> G[✅ Portable]
    E --> H[✅ Global Suspend]
    
    B --> I[💰 High Cost]
    C --> I
    D --> I
    
    F --> J[💰 Lower Cost]
    G --> J
    H --> J
    
    style A fill:#ff6b6b
    style E fill:#96ceb4
    style I fill:#ff6b6b
    style J fill:#96ceb4
```

</div>

### 🎯 **Neutral & Portable**
- Works across all platforms
- No vendor lock-in
- Open standards

### ⚡ **Real-time Enforcement**
- Sub-100ms policy checks
- Global suspend in seconds
- Edge-deployed for speed

### 🔐 **Enterprise Ready**
- Multi-level assurance
- Complete audit trails
- Compliance built-in

### 🛠️ **Developer Friendly**
- Simple APIs
- Rich SDKs
- GitHub Actions ready

## 🚀 Get Started Today

<div align="center">

### 🎯 **For Developers**
[![Try APort](https://img.shields.io/badge/Try%20APort-Now-brightgreen?style=for-the-badge&logo=rocket)](https://aport.io/dashboard)

### 🏢 **For Platforms**
[![Contact Sales](https://img.shields.io/badge/Contact%20Sales-Let's%20Talk-blue?style=for-the-badge&logo=mail)](mailto:sales@aport.io)

### 💬 **Join Community**
[![Discord](https://img.shields.io/badge/Discord-Join%20Us-blue?style=for-the-badge&logo=discord)](https://discord.gg/aport)

</div>

## 📚 Resources

- 📖 **[Documentation](https://aport.io/docs)** - Complete guides and API reference
- 🎮 **[Playground](https://aport.io/playground)** - Try APort in your browser
- 📺 **[Video Tutorials](https://youtube.com/@aport)** - Step-by-step guides
- 💡 **[Examples](https://github.com/aporthq/examples)** - Real-world implementations
- 🐛 **[Report Issues](https://github.com/aporthq/agent-passport/issues)** - Help us improve

## 🤝 Contributing

We love contributions! Whether it's:

- 🐛 **Bug fixes**
- ✨ **New features** 
- 📚 **Documentation**
- 🎨 **Design improvements**
- 🧪 **Tests**

Check out our [Contributing Guide](CONTRIBUTING.md) to get started.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**🛡️ Secure your AI agents. Trust but verify.**

[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=social&logo=github)](https://github.com/aporthq)
[![Twitter](https://img.shields.io/badge/Twitter-Follow-blue?style=social&logo=twitter)](https://twitter.com/aporthq)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Follow-blue?style=social&logo=linkedin)](https://linkedin.com/company/aporthq)

Made with ❤️ by the APort team

</div>
