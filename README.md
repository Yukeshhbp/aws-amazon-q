# 🚀 Accelerate AWS Architecture Diagramming with Amazon Q CLI & MCP Server in GitHub Codespace

This repository shows how to set up **Amazon Q Developer CLI** inside a **GitHub Codespace**, connect it with AWS MCP Servers for architecture diagramming, and use AI-assisted prompts to generate high-quality AWS Architecture Diagrams.

---

## 📦 1. Install Amazon Q Developer CLI in GitHub Codespace

The Codespace container is an **Ubuntu-based Linux VM**, so we can follow the standard Linux (headless) install for Amazon Q.

---

### 1️⃣ Open the Codespace Terminal
In the browser, press <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>`</kbd>  
Or go to **Terminal → New Terminal**.

---

### 2️⃣ Install Required Utilities
```bash
sudo apt-get update
sudo apt-get install -y unzip curl
````

---

### 3️⃣ Download the Latest Headless Build

```bash
curl --proto '=https' --tlsv1.2 -sSf \
  https://desktop-release.codewhisperer.us-east-1.amazonaws.com/latest/q-x86_64-linux-musl.zip \
  -o /tmp/q.zip
```

---

### 4️⃣ Unpack and Run the Installer

```bash
cd /tmp
unzip q.zip
chmod +x q/install.sh
./q/install.sh
```

**When prompted:**

1. **Add Amazon Q to your shell’s PATH?** → Type `y`
2. **Login method?** → Choose **Use for Free with Builder ID** and complete the browser login.

---

## 💬 5. Start Amazon Q Chat

Once installed, start an interactive Amazon Q session:

```bash
q chat
```

Inside the chat, provide this initial context to set up MCP servers:

```
I want to setup AWS diagram MCP server. Execute these steps:
1. Install Python 3.10
2. Install AWS Diagram MCP server package from here: https://awslabs.github.io/mcp/servers/aws-diagram-mcp-server/
3. Install AWS Documentation MCP server package from here: https://awslabs.github.io/mcp/servers/aws.documentation-mcp-server/
4. Create necessary MCP configuration files at ~/.aws/amazonq/mcp.json
```

---

## 🔄 6. Restart Amazon Q & Verify MCP Tools

To restart Amazon Q:

```bash
/quit
q chat
```

When Amazon Q restarts, it should display MCP servers like this:

<img width="593" height="230" alt="image" src="https://github.com/user-attachments/assets/bfe557f7-3b78-4530-946f-09e9b3cd4bd7" />


✅ **Expected:**

* `awslabs.aws-diagram-mcp-server` loaded
* `awslabs.aws-documentation-mcp-server` loaded

⚠ If tools don’t load, give Amazon Q this JSON:

```json
{
    "mcpServers": {
        "awslabs.aws-diagram-mcp-server": {
            "command": "uvx",
            "args": ["awslabs.aws-diagram-mcp-server"],
            "env": {
                "FASTMCP_LOG_LEVEL": "ERROR"
            },
            "autoApprove": [],
            "disabled": false
        },
        "awslabs.aws-documentation-mcp-server": {
            "command": "uvx",
            "args": ["awslabs.aws-documentation-mcp-server@latest"],
            "env": {
                "FASTMCP_LOG_LEVEL": "ERROR"
            },
            "autoApprove": [],
            "disabled": false
        }
    }
}
```

And add it to:

```
~/.aws/amazonq/mcp.json
```

---

## 🖼 7. Generate an AWS Architecture Diagram

### Step 1 — Prepare a High-Quality Prompt

Use any AI chatbot (**ChatGPT**, **Gemini**, **Perplexity**, etc.) to refine your architecture request.
Start with:

```
I need to create a prompt that...
```

Include:

* **Requirements** (e.g., serverless, multi-region, secure)
* **Flow** (e.g., user → API Gateway → Lambda → DynamoDB)
* **Logical components**
* **Constraints**

The goal is to get the AI to generate a **clear, detailed, accurate** prompt.

---

### Step 2 — Send the Prompt to Amazon Q

Paste your final prompt inside `q chat`.

Amazon Q will:

* Generate a **`.png` diagram** inside the `generated-diagrams` folder.
* Provide a **diagram description** in the terminal.

---

### Step 3 — View the Diagram

In your Codespace, open the `generated-diagrams` folder to see the AWS Architecture Diagram.
You can preview it directly inside GitHub Codespaces.

---

## 📚 References

* [Amazon Q Developer CLI Documentation](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line.html)
* [AWS Diagram MCP Server](https://awslabs.github.io/mcp/servers/aws-diagram-mcp-server/)
* [AWS Documentation MCP Server](https://awslabs.github.io/mcp/servers/aws.documentation-mcp-server/)

---

**Now you’re ready to create clear, precise AWS Architecture Diagrams directly from your GitHub Codespace using Amazon Q!**

```

---

Do you want me to **embed the provided screenshot directly** in the README so it displays without needing the file in the repo, or keep it as a relative image link so it works when you commit it along with the PNG?
```
