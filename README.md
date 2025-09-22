# 🛡️ APort - Agent Identity & Policy Enforcement

<div align="center">

![APort Logo](https://img.shields.io/badge/APort-Agent%20Passport-06b6d4?style=for-the-badge&logo=shield&logoColor=white)

**The neutral, portable passport + verify + suspend rail for AI agents**

[![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-Ready-10b981?style=flat-square&logo=github-actions)](https://github.com/aporthq/policy-verify-action)
[![API Status](https://img.shields.io/badge/API-Live-10b981?style=flat-square&logo=api)](https://api.aport.io)
[![License](https://img.shields.io/badge/License-MIT-f59e0b?style=flat-square)](LICENSE)

[🌐 Website](https://aport.io) • [📚 Docs](https://aport.io/docs) • [🚀 Try Now](https://aport.io/dashboard) • [💬 Support](mailto:support@aport.io)

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
    A[🤖 AI Agent<br/>with Passport] --> B[🛡️ APort Verify]
    B --> C{Policy Check}
    C -->|✅ Allowed| D[✅ Action Proceeds]
    C -->|❌ Blocked| E[🚫 Action Blocked]
    
    F[📋 Policy Pack] --> B
    G[⚡ Global Suspend] --> B
    
    style A fill:#06b6d4,color:#ffffff
    style B fill:#10b981,color:#ffffff
    style D fill:#10b981,color:#ffffff
    style E fill:#ef4444,color:#ffffff
    style F fill:#8b5cf6,color:#ffffff
    style G fill:#f59e0b,color:#ffffff
```

**APort provides a neutral, portable identity and policy enforcement layer for AI agents across all platforms.**

</div>

## 🚀 Quick Start

### 1. Create Your Agent Passport

```bash
# Create a template passport via API
curl -X POST "https://api.aport.io/api/admin/create" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_ADMIN_API_KEY" \
  -d '{
    "name": "HappyRefunds Bot",
    "role": "Support Refunds",
    "description": "Refund helper for customer support",
    "capabilities": [{"id": "payments.refund", "params": {}}],
    "limits": {
      "refund_usd_max_per_tx": 50,
      "refund_usd_daily_cap": 200
    },
    "regions": ["US", "CA"],
    "contact": "team@aport.io",
    "links": {
      "homepage": "https://aport.io",
      "repo": "https://github.com/aporthq/agent-passport"
    },
    "kind": "template",
    "controller_type": "org",
    "status": "active"
  }'
```

### 2. Add Policy Enforcement

```yaml
# .github/workflows/aport-verify.yml
name: APort Verify PR
on: [pull_request]

jobs:
  verify:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: aporthq/policy-verify-action@v1
        with:
          agent-id: ${{ secrets.APORT_AGENT_ID }}
          policy-pack: 'repo.v1'
```

### 3. Integrate with Your App

```javascript
// Express.js with Policy Pack middleware
const { requirePolicy } = require("@aport/middleware-express");

// Apply policy enforcement to refunds endpoint
app.post("/api/refunds", 
  requirePolicy("refunds.v1", "agt_inst_xyz789"),
  async (req, res) => {
    // Your business logic - policy already verified!
    const refund = await processRefund(req.body);
    res.json({ success: true, refund });
  }
);
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
    F --> F1[Slack<br/>Teams<br/>Discord]
    
    style A fill:#06b6d4,color:#ffffff
    style B fill:#10b981,color:#ffffff
    style C fill:#f59e0b,color:#ffffff
    style D fill:#8b5cf6,color:#ffffff
    style E fill:#ef4444,color:#ffffff
    style F fill:#06b6d4,color:#ffffff
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
// Express.js with Policy Pack middleware
const { requirePolicy } = require("@aport/middleware-express");

app.post("/api/refunds", 
  requirePolicy("refunds.v1", "agt_inst_xyz789"),
  async (req, res) => {
    // Policy already verified! Check specific limits
    const passport = req.policyResult.passport;
    
    if (req.body.amount > passport.limits.refund_usd_max_per_tx) {
      return res.status(403).json({
        error: "Refund exceeds limit",
        requested: req.body.amount,
        limit: passport.limits.refund_usd_max_per_tx
      });
    }

    // Process refund safely
    const refund = await stripe.refunds.create({
      amount: req.body.amount,
      payment_intent: req.body.payment_intent
    });
    
    res.json({ success: true, refund });
  }
);
```

### 🔀 GitHub PR Automation
```yaml
# .github/workflows/aport-verify.yml
name: APort Verify PR
on: [pull_request]

jobs:
  verify:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Verify via APort
        run: |
          BODY=$(jq -n \
            --arg agent_id "$APORT_AGENT_ID" \
            --arg repo "$GITHUB_REPOSITORY" \
            --arg base "${{ github.event.pull_request.base.ref }}" \
            --arg head "${{ github.event.pull_request.head.ref }}" \
            --argjson files_changed "${{ steps.changed-files.outputs.files }}" \
            '{
              agent_id: $agent_id,
              context: {
                repo: $repo,
                base: $base,
                head: $head,
                files_changed: $files_changed,
                author: "${{ github.event.pull_request.user.login }}"
              }
            }')
          
          curl -s -X POST "https://api.aport.io/api/verify/policy/repo.v1" \
            -H "Content-Type: application/json" \
            -d "$BODY" | tee result.json
        env:
          APORT_AGENT_ID: ${{ secrets.APORT_AGENT_ID }}
```

### 📊 Data Export Control
```javascript
// FastAPI with Policy Pack middleware
from fastapi import FastAPI, Request
from aport.middleware import require_policy

@app.post("/api/data/export")
@require_policy("data_export.v1", "agt_inst_xyz789")
async def export_data(request: Request, export_data: dict):
    passport = request.state.policy_result.passport
    
    # Check PII permission
    if export_data.get("include_pii") and not passport.limits.allow_pii:
        raise HTTPException(403, {
            "error": "PII export not allowed",
            "agent_id": passport.agent_id,
            "upgrade_instructions": "Request PII export capability from your administrator"
        })
    
    # Check row limit
    if export_data["rows"] > passport.limits.max_rows_per_export:
        raise HTTPException(403, {
            "error": "Export exceeds row limit",
            "requested": export_data["rows"],
            "limit": passport.limits.max_rows_per_export
        })
    
    # Process export safely
    return {"success": True, "export_id": f"exp_{int(time.time())}"}
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
    
    style A fill:#ef4444,color:#ffffff
    style E fill:#10b981,color:#ffffff
    style I fill:#ef4444,color:#ffffff
    style J fill:#10b981,color:#ffffff
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

## 👥 For Every Role

<div align="center">

### 🤖 **Agent Builders**
Create and manage AI agent passports with capabilities and limits

```bash
# Issue a template passport
curl -X POST "https://api.aport.io/api/admin/create" \
  -H "Authorization: Bearer YOUR_ADMIN_API_KEY" \
  -d '{
    "name": "HappyRefunds Bot",
    "role": "Support Refunds", 
    "capabilities": [{"id": "payments.refund", "params": {}}],
    "limits": {"refund_usd_max_per_tx": 50}
  }'
```

### 🏢 **Platform Developers**
Integrate APort middleware to protect sensitive operations

```javascript
// Express.js middleware
const { requirePolicy } = require("@aport/middleware-express");

app.post("/api/refunds", 
  requirePolicy("refunds.v1", "agt_inst_xyz789"),
  async (req, res) => {
    // Policy already verified!
    res.json({ success: true, refund: await processRefund(req.body) });
  }
);
```

### 🔧 **DevOps Engineers**
Add GitHub Actions for automated policy verification

```yaml
# .github/workflows/aport-verify.yml
name: APort Verify PR
on: [pull_request]
jobs:
  verify:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: aporthq/policy-verify-action@v1
        with:
          agent-id: ${{ secrets.APORT_AGENT_ID }}
          policy-pack: 'repo.v1'
```

### 🎯 **No-Code Platforms**
Mint instance passports for each tenant installation

```bash
# Mint instance passport on tenant install
curl -X POST "https://api.aport.io/api/passports/agt_tmpl_abc123/instances" \
  -H "Authorization: Bearer YOUR_PLATFORM_API_KEY" \
  -d '{
    "platform_id": "gorgias",
    "controller_id": "org_acme",
    "tenant_ref": "store_987",
    "overrides": {"limits": {"refund_usd_max_per_tx": 50}}
  }'
```

</div>

## 🚀 Get Started Today

<div align="center">

### 🎯 **For Developers**
[![Try APort](https://img.shields.io/badge/Try%20APort-Now-10b981?style=for-the-badge&logo=rocket)](https://aport.io/dashboard)

### 🏢 **For Platforms**
[![Contact Sales](https://img.shields.io/badge/Contact%20Sales-Let's%20Talk-06b6d4?style=for-the-badge&logo=mail)](mailto:team@aport.io)

### 💬 **Get Support**
[![Support](https://img.shields.io/badge/Support-Help%20Center-06b6d4?style=for-the-badge&logo=mail)](mailto:support@aport.io)

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
[![Twitter](https://img.shields.io/badge/Twitter-Follow-06b6d4?style=social&logo=twitter)](https://twitter.com/aporthq)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Follow-06b6d4?style=social&logo=linkedin)](https://linkedin.com/company/aporthq)

Made with ❤️ by the APort team

</div>
