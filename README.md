# 📊 Observability & Evaluations Workshop

[![Microsoft Foundry](https://img.shields.io/badge/Microsoft-Foundry-blue?style=for-the-badge&logo=microsoft)](https://ai.azure.com)
[![Python](https://img.shields.io/badge/Python-3.10+-green?style=for-the-badge&logo=python)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Lab-orange?style=for-the-badge&logo=jupyter)](https://jupyter.org)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

**Hands-on workshop for AI agent telemetry, evaluation, and security testing with Microsoft Foundry**

*Learn to build observable, evaluable, and secure AI agents through real-world financial services use cases.*

---

## 📑 Table of Contents

- [🎯 Overview](#-overview)
- [📁 Repository Structure](#-repository-structure)
- [🚀 Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Step 1: Repository Setup](#step-1-repository-setup)
  - [Step 2: Environment Setup](#step-2-environment-setup)
  - [Step 3: Configure Environment Variables](#step-3-configure-environment-variables)
  - [Step 4: Microsoft Foundry Setup](#step-4-microsoft-foundry-setup)
  - [Step 5: Required Azure RBAC Roles](#step-5-required-azure-rbac-roles)
- [📚 Learning Path](#-learning-path)
- [📖 Notebook Details](#-notebook-details)
- [🔑 Key Evaluators Reference](#-key-evaluators-reference)
- [🛠️ Troubleshooting](#️-troubleshooting)
- [📚 Additional Resources](#-additional-resources)

---

## 🎯 Overview

This workshop teaches you how to build **robust AI agents** with proper observability and evaluation capabilities using Microsoft Foundry. For enterprise applications, this is critical for:

- **Compliance & Governance** — Full audit trails of AI interactions
- **Quality Assurance** — Safety and quality evaluation of agent responses
- **Operational Excellence** — Performance monitoring and debugging
- **Security** — Proactive vulnerability detection through red team testing
- **Continuous Improvement** — Data-driven agent optimization

All notebooks feature **financial services industry (FSI) use cases** including advisory services, banking operations, and compliance monitoring.

| Module | Topics | Technology |
|--------|--------|------------|
| **Telemetry** | Azure Monitor tracing, custom spans, content recording | OpenTelemetry, Application Insights |
| **Evaluation** | Built-in evaluators, safety checks, quality metrics | Foundry Evals API |
| **Tool Evaluation** | Function tool testing, tool call accuracy | FunctionTool, azure_ai_responses |
| **Security** | Red team testing, adversarial attacks, vulnerability detection | Red Team API, Attack Strategies |

> **🎓 Format**: Hands-on Jupyter notebooks  
> **🎯 Audience**: Developers, AI practitioners, and solution architects  
> **⏱️ Duration**: ~2.5 hours total

---

## 📁 Repository Structure

```
observability-and-evaluations/
│
├── 1-telemetry.ipynb                          # Azure Monitor telemetry & tracing
├── 2-agent-evaluation.ipynb                   # Built-in evaluators (safety, fluency, adherence)
├── 3-agent-evaluation-with-function-tools.ipynb  # Tool-enabled agent evaluation
├── 4-tool-call-accuracy-evaluation.ipynb      # Tool selection accuracy testing
├── 5-red-team-security-testing.ipynb          # Adversarial red team security scans
│
├── red_team_results/                          # Red team output artifacts
├── .env.example                               # Environment template
├── requirements.txt                           # Pinned dependencies
└── README.md                                  # This file
```

---

## 💼 Notebook Use Cases

| # | Notebook | Use Case | Key Concept |
|---|----------|----------|-------------|
| 1 | [1-telemetry.ipynb](observability-and-evaluations/1-telemetry.ipynb) | Wealth Management Advisory Monitoring | Azure Monitor tracing, custom spans, Application Insights |
| 2 | [2-agent-evaluation.ipynb](observability-and-evaluations/2-agent-evaluation.ipynb) | Loan Advisory Quality Testing | Built-in evaluators (violence, fluency, task adherence) |
| 3 | [3-agent-evaluation-with-function-tools.ipynb](observability-and-evaluations/3-agent-evaluation-with-function-tools.ipynb) | Banking Assistant with Account Lookup | Function tool evaluation, `azure_ai_responses` data source |
| 4 | [4-tool-call-accuracy-evaluation.ipynb](observability-and-evaluations/4-tool-call-accuracy-evaluation.ipynb) | Banking Operations Tool Validation | `builtin.tool_call_accuracy`, JSONL inline data |
| 5 | [5-red-team-security-testing.ipynb](observability-and-evaluations/5-red-team-security-testing.ipynb) | Banking AI Security Assessment | Red team attacks (Flip, Base64), safety evaluators |

---

## 🚀 Getting Started

### Prerequisites

| Requirement | Details |
|-------------|---------|
| **Python** | 3.10 or later |
| **Azure Subscription** | Access to Microsoft Foundry |
| **Azure CLI** | 2.60+ with active `az login` session |
| **Azure OpenAI** | Deployed model (`gpt-4o` recommended) |
| **VS Code** | With Python and Jupyter extensions |
| **Optional** | Application Insights resource for telemetry (notebook 1) |

### Step 1: Repository Setup

```powershell
# Clone the repository
git clone https://github.com/dhangerkapil/agentic-ai-immersion.git
cd agentic-ai-immersion

# Verify Python version
python --version  # Python 3.10+ required
```

### Step 2: Environment Setup

```powershell
# Create and activate virtual environment
python -m venv .venv
.\.venv\Scripts\activate

# Install dependencies (versions are pinned for consistency)
pip install -r requirements.txt
```

### Step 3: Configure Environment Variables

1. Copy `.env.example` to `.env` in the repository root
2. Update with your Azure resources:

```env
# Required for all notebooks
AI_FOUNDRY_PROJECT_ENDPOINT=https://<your-foundry-resource>.services.ai.azure.com/api/projects/<your-project-name>
TENANT_ID=<your-azure-tenant-id>
AZURE_AI_MODEL_DEPLOYMENT_NAME=gpt-4o

# Required for observability (notebook 1)
AZURE_TRACING_GEN_AI_CONTENT_RECORDING_ENABLED=true
AZURE_SDK_TRACING_IMPLEMENTATION=opentelemetry

# Optional - for local evaluations (uses token-based auth via DefaultAzureCredential)
AZURE_OPENAI_ENDPOINT=https://<your-openai-resource>.openai.azure.com/
AZURE_OPENAI_DEPLOYMENT=<your-deployment-name>
```

> **Note:** This project uses **token-based authentication** via `DefaultAzureCredential`. No API keys are needed. Make sure you are logged in using one of the methods below.

### Azure Sign-In

You can authenticate with Azure using **either** of these methods:

- **VS Code Command Palette**:  
  Press `Ctrl+Shift+P`, type **Azure: Sign In**, and select it. A browser window will open for you to complete the login. If you need to target a specific tenant, choose **Azure: Sign In to Directory...** instead.

- **Azure CLI**:
  ```bash
  az login
  # Or, to specify a tenant:
  az login --tenant YOUR_TENANT_ID
  ```

After signing in, verify your account is correct:
```bash
az account show
```

### Step 4: Microsoft Foundry Setup

1. **Create Microsoft Foundry Resource** — [Azure Portal](https://portal.azure.com/#create/Microsoft.CognitiveServicesAIFoundry)
2. **Deploy Models** — `gpt-4o` (required for all notebooks)
3. **Connect Application Insights** — Required for notebook 1 (telemetry)

For detailed setup instructions, see [Microsoft Foundry Documentation](https://learn.microsoft.com/en-us/azure/ai-foundry/).

### Step 5: Required Azure RBAC Roles

Assign the following role to your user identity on the AI Foundry resource:

| Role | Resource | Purpose | Notebooks |
|------|----------|---------|-----------|
| **Azure AI User** | AI Services / Foundry Resource | Access models, agents, evaluations, and all Foundry V2 capabilities | All |
| **Monitoring Metrics Publisher** *(optional)* | Application Insights Resource | Required only if you enable Entra ID-based telemetry ingestion (see notebook 1, commented-out `credential` parameter) | 1 |

#### Role Assignment Commands

```powershell
# Get your user principal ID
$USER_PRINCIPAL_ID = (az ad signed-in-user show --query id -o tsv)

# Get resource scope (replace with your values)
$RESOURCE_SCOPE = "/subscriptions/<sub-id>/resourceGroups/<rg>/providers/Microsoft.CognitiveServices/accounts/<your-foundry-resource>"

# Required for all notebooks
az role assignment create --role "Azure AI User" --assignee $USER_PRINCIPAL_ID --scope $RESOURCE_SCOPE

# OPTIONAL: Only needed if you enable Entra ID auth for Application Insights in notebook 1
# $APP_INSIGHTS_SCOPE = "/subscriptions/<sub-id>/resourceGroups/<rg>/providers/Microsoft.Insights/components/<your-app-insights>"
# az role assignment create --role "Monitoring Metrics Publisher" --assignee $USER_PRINCIPAL_ID --scope $APP_INSIGHTS_SCOPE
```

> **⚠️ Note:** Role assignments can take **5-10 minutes** to propagate. If you encounter permission errors, wait and retry.

---

## 📚 Learning Path

Follow this structured path to master observability and evaluation concepts:

| Step | Focus | Notebook | Time |
|------|-------|----------|------|
| 1 | **Telemetry Setup** | `1-telemetry.ipynb` | 20 min |
| 2 | **Basic Evaluation** | `2-agent-evaluation.ipynb` | 25 min |
| 3 | **Tool-Enabled Agents** | `3-agent-evaluation-with-function-tools.ipynb` | 30 min |
| 4 | **Tool Accuracy** | `4-tool-call-accuracy-evaluation.ipynb` | 25 min |
| 5 | **Security Testing** | `5-red-team-security-testing.ipynb` | 30 min |

**Progression:**
```
Telemetry → Basic Evaluation → Tool Evaluation → Tool Accuracy → Red Team
    ↓              ↓                  ↓                ↓              ↓
 Monitoring    Safety checks     Function tools    Selection    Security
```

---

## 📖 Notebook Details

### 1. Telemetry (`1-telemetry.ipynb`)

Implement **telemetry and tracing** for AI agents with Azure Monitor.

| Feature | Description |
|---------|-------------|
| **Use Case** | Wealth Management Advisory Agent with Monitoring |
| **Azure Monitor Setup** | Configure OpenTelemetry with Application Insights |
| **Content Recording** | Capture prompts and responses for compliance |
| **Custom Trace Spans** | Add business context (client ID, query category) |
| **Compliance Tracking** | Full audit trail of agent interactions |

**Key APIs:**
```python
configure_azure_monitor(connection_string=...)
tracer = trace.get_tracer("agent-name")
with tracer.start_as_current_span("operation") as span:
    span.set_attribute("client_id", "C-12345")
```

---

### 2. Agent Evaluation (`2-agent-evaluation.ipynb`)

**Evaluate AI agents** using Microsoft Foundry's built-in evaluators.

| Feature | Description |
|---------|-------------|
| **Use Case** | Loan Advisory Agent Quality Testing |
| **Built-in Evaluators** | Violence detection, fluency, task adherence |
| **Test Queries** | Business-relevant advisory questions |
| **Results Analysis** | Detailed metrics and report URLs |

**Key APIs:**
```python
eval_object = openai_client.evals.create(
    name="Agent Evaluation",
    data_source_config=data_source_config,
    testing_criteria=testing_criteria,
)
eval_run = openai_client.evals.runs.create(eval_id=eval_object.id, ...)
```

---

### 3. Agent Evaluation with Function Tools (`3-agent-evaluation-with-function-tools.ipynb`)

**Evaluate agents with function tools** for banking account lookup operations.

| Feature | Description |
|---------|-------------|
| **Use Case** | Banking Assistant with Account Balance Lookup |
| **Function Tools** | `get_account_balance`, `get_recent_transactions` |
| **Tool Processing** | Handle function calls and return results to agent |
| **Data Source** | `azure_ai_responses` — evaluate specific response by ID |

**Key APIs:**
```python
get_balance_tool = FunctionTool(name="get_account_balance", parameters={...}, strict=True)
# Process function calls, then evaluate response
data_source = {"type": "azure_ai_responses", ...}
```

---

### 4. Tool Call Accuracy (`4-tool-call-accuracy-evaluation.ipynb`)

Evaluate **tool call accuracy** — whether agents select the correct tools with proper parameters.

| Feature | Description |
|---------|-------------|
| **Use Case** | Banking Operations Tool Selection |
| **Evaluator** | `builtin.tool_call_accuracy` |
| **5 Test Scenarios** | Balance inquiry, wire transfer, fraud report, multi-tool, loan application |
| **Data Source** | Inline JSONL with tool definitions and expected calls |

**Key APIs:**
```python
testing_criteria = [{
    "type": "azure_ai_evaluator",
    "evaluator_name": "builtin.tool_call_accuracy",
    "data_mapping": {
        "query": "{{item.query}}",
        "tool_definitions": "{{item.tool_definitions}}",
        "tool_calls": "{{item.tool_calls}}",
    },
}]
```

---

### 5. Red Team Security Testing (`5-red-team-security-testing.ipynb`)

Perform **Red Team security scans** to identify AI vulnerabilities through adversarial attacks.

| Feature | Description |
|---------|-------------|
| **Use Case** | Banking AI Security Assessment |
| **Attack Strategies** | Flip, Base64 encoding attacks |
| **Safety Evaluators** | Prohibited actions, task adherence, sensitive data leakage |
| **Target** | Foundry Agent with banking persona |

**Key APIs:**
```python
red_team = client.evals.create(
    name="Red Team Evaluation",
    data_source_config={"type": "azure_ai_source", "scenario": "red_team"},
    testing_criteria=[...],
)
eval_run = client.evals.runs.create(
    eval_id=red_team.id,
    data_source={"type": "azure_ai_red_team", ...},
)
```

---

## 🔑 Key Evaluators Reference

### Built-in Evaluators

| Evaluator | Purpose | Use Case |
|-----------|---------|----------|
| `builtin.violence` | Detect violent content | Ensure safe customer interactions |
| `builtin.fluency` | Measure response quality | Professional communication standards |
| `builtin.task_adherence` | Check task completion | Accurate advisory and operational guidance |
| `builtin.tool_call_accuracy` | Validate correct tool usage | Proper banking operation selection |
| `builtin.prohibited_actions` | Detect prohibited actions | Prevent unauthorized transactions |
| `builtin.sensitive_data_leakage` | Identify data leakage | Protect customer PII |

### Data Source Types

| Type | Use Case | Notebooks |
|------|----------|-----------|
| `azure_ai_target_completions` | Evaluate agent with test queries | 2 |
| `azure_ai_responses` | Evaluate specific response by ID | 3 |
| `jsonl` (inline) | Provide test data directly in code | 4 |
| `azure_ai_red_team` | Red team adversarial attacks | 5 |

### Evaluation Flow

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│  Create Eval    │────▶│   Run Eval       │────▶│  Analyze        │
│  (criteria)     │     │   (test data)    │     │  Results        │
└─────────────────┘     └──────────────────┘     └─────────────────┘
        │                        │                       │
        ▼                        ▼                       ▼
   Define what           Execute against          View metrics,
   to measure            agent/data               report URLs
```

---

## 🛠️ Troubleshooting

| Issue | Solution |
|-------|----------|
| **Authentication failures** | Re-run `az login --use-device-code` |
| **Kernel issues** | `python -m ipykernel install --user --name=ai-foundry-lab` then reload VS Code |
| **Environment activation** | `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` |
| **Trace IDs showing as zeros** | Use `telemetry.get_application_insights_connection_string()` |
| **Missing environment variables** | Verify `.env` file in the repository root directory |
| **Evaluation stuck in "queued"** | Check model deployment quota and availability |
| **Package import errors** | Run `pip install -r requirements.txt` in the activated venv |
| **Tool call accuracy errors** | With `strict=True`, ALL properties must be in the `required` array |
| **Application Insights delay** | Use Live Metrics Stream for real-time debugging |

---

## 📚 Additional Resources

### Documentation

| Resource | Link |
|----------|------|
| **Microsoft Foundry Docs** | [learn.microsoft.com/azure/ai-foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/) |
| **Foundry Evaluation Concepts** | [learn.microsoft.com/.../evaluation](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/evaluation) |
| **Azure AI Evaluation SDK** | [learn.microsoft.com/python/api/azure-ai-evaluation](https://learn.microsoft.com/python/api/azure-ai-evaluation/) |
| **OpenTelemetry with Azure Monitor** | [learn.microsoft.com/.../opentelemetry-overview](https://learn.microsoft.com/en-us/azure/azure-monitor/app/opentelemetry-overview) |
| **Function Calling Best Practices** | [learn.microsoft.com/.../function-calling](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/function-calling) |
| **AI Red Teaming (Cloud)** | [learn.microsoft.com/.../run-ai-red-teaming-cloud](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/develop/run-ai-red-teaming-cloud) |

### GitHub Samples

- [Agent Evaluation Samples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-projects/samples/evaluations)
- [Telemetry Samples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-projects/samples/telemetry)
- [Agentic Evaluators](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-projects/samples/evaluations/agentic_evaluators)
- [Red Team Samples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-projects/samples/red_team)

---

## 📄 License

**License:** MIT License  
**Repository:** [github.com/dhangerkapil/agentic-ai-immersion](https://github.com/dhangerkapil/agentic-ai-immersion)

---

<div align="center">

**Built with ❤️ for the AI Developer Community**

*Happy Learning! 🚀*

</div>
