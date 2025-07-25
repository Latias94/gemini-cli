# Gemini CLI

[![Gemini CLI CI](https://github.com/google-gemini/gemini-cli/actions/workflows/ci.yml/badge.svg)](https://github.com/google-gemini/gemini-cli/actions/workflows/ci.yml)

![Gemini CLI Screenshot](./docs/assets/gemini-screenshot.png)

This repository contains the Gemini CLI, a command-line AI workflow tool that connects to your
tools, understands your code and accelerates your workflows.

With the Gemini CLI you can:

- Query and edit large codebases in and beyond Gemini's 1M token context window.
- Generate new apps from PDFs or sketches, using Gemini's multimodal capabilities.
- Automate operational tasks, like querying pull requests or handling complex rebases.
- Use tools and MCP servers to connect new capabilities, including [media generation with Imagen,
  Veo or Lyria](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia)
- Ground your queries with the [Google Search](https://ai.google.dev/gemini-api/docs/grounding)
  tool, built in to Gemini.

## Quickstart

1. **Prerequisites:** Ensure you have [Node.js version 20](https://nodejs.org/en/download) or higher installed.
2. **Run the CLI:** Execute the following command in your terminal:

   ```bash
   npx https://github.com/google-gemini/gemini-cli
   ```

   Or install it with:

   ```bash
   npm install -g @google/gemini-cli
   gemini
   ```

3. **Pick a color theme**
4. **Authenticate:** When prompted, choose your preferred AI provider:
   - **Login with Google:** Sign in with your personal Google account for up to 60 model requests per minute and 1,000 model requests per day using Gemini.
   - **Gemini API Key:** Use a Google AI Studio API key for higher limits.
   - **DeepSeek API Key:** Use DeepSeek's models with your DeepSeek API key.
   - **OpenAI-like API:** Use any OpenAI-compatible API (DeepSeek, OpenAI, Volcengine, etc.)
   - **Vertex AI:** For enterprise Google Cloud users.

You are now ready to use the Gemini CLI!

## Installing from Source (Development/Fork)

If you have forked this repository or want to install a locally modified version:

### Method 1: Using npm pack (Recommended for testing releases)

Best for: Testing the final packaged version before publishing

1. **Clone and build the project:**
   ```bash
   git clone https://github.com/your-username/gemini-cli.git  # Or your fork's URL
   cd gemini-cli
   npm install
   npm run build
   ```

2. **Package and install globally:**
   ```bash
   npm pack
   npm install -g google-gemini-cli-*.tgz
   ```

3. **Verify installation:**
   ```bash
   gemini --version
   ```

**Updating:** When you make changes, rebuild and repackage:
```bash
npm run build
npm pack
npm install -g google-gemini-cli-*.tgz
```

### Method 2: Direct installation from directory (Recommended for development)

Best for: Frequent code changes and rapid iteration

```bash
# Clone and build the project
git clone https://github.com/your-username/gemini-cli.git  # Or your fork's URL
cd gemini-cli
npm install
npm run build

# Install directly from directory
npm install -g .
```

**Updating:** When you make changes, just rebuild and reinstall:
```bash
npm run build
npm install -g .
```

### For advanced use or increased limits:

#### Using Gemini API

If you need to use a specific model or require a higher request capacity, you can use an API key:

1. Generate a key from [Google AI Studio](https://aistudio.google.com/apikey).
2. Set it as an environment variable in your terminal. Replace `YOUR_API_KEY` with your generated key.

   ```bash
   export GEMINI_API_KEY="YOUR_API_KEY"
   ```

3. (Optionally) Upgrade your Gemini API project to a paid plan on the API key page (will automatically unlock [Tier 1 rate limits](https://ai.google.dev/gemini-api/docs/rate-limits#tier-1))

### Use a Vertex AI API key:

The Vertex AI provides [free tier](https://cloud.google.com/vertex-ai/generative-ai/docs/start/express-mode/overview) using express mode for Gemini 2.5 Pro, control over which model you use, and access to higher rate limits with a billing account:

1. Generate a key from [Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/start/api-keys).
2. Set it as an environment variable in your terminal. Replace `YOUR_API_KEY` with your generated key and set GOOGLE_GENAI_USE_VERTEXAI to true

   ```bash
   export GOOGLE_API_KEY="YOUR_API_KEY"
   export GOOGLE_GENAI_USE_VERTEXAI=true
   ```

3. (Optionally) Add a billing account on your project to get access to [higher usage limits](https://cloud.google.com/vertex-ai/generative-ai/docs/quotas)
#### Using DeepSeek API

To use DeepSeek's models (including DeepSeek-V3 and DeepSeek-R1):

1. Generate a key from [DeepSeek Platform](https://platform.deepseek.com/).
2. Set it as an environment variable in your terminal. Replace `YOUR_DEEPSEEK_API_KEY` with your generated key.

   ```bash
   export DEEPSEEK_API_KEY="YOUR_DEEPSEEK_API_KEY"
   ```

3. Optionally specify the model (defaults to `deepseek-chat`):

   ```bash
   export GEMINI_MODEL="deepseek-reasoner"  # For DeepSeek-R1
   ```

#### Using OpenAI-like API

To use any OpenAI-compatible API service (DeepSeek, OpenAI, Volcengine, etc.):

Set the required environment variables:

   ```bash
   export OPENAI_LIKE_API_KEY="YOUR_API_KEY"
   export OPENAI_LIKE_BASE_URL="YOUR_API_BASE_URL"
   export OPENAI_LIKE_MODEL="YOUR_MODEL_NAME"  # Optional
   ```

For other authentication methods, including Google Workspace accounts, see the [authentication](./docs/cli/authentication.md) guide.

## Examples

Once the CLI is running, you can start interacting with Gemini from your shell.

You can start a project from a new directory:

```sh
cd new-project/
gemini
> Write me a Gemini Discord bot that answers questions using a FAQ.md file I will provide
```

Or work with an existing project:

```sh
git clone https://github.com/google-gemini/gemini-cli
cd gemini-cli
gemini
> Give me a summary of all of the changes that went in yesterday
```

### Next steps

- Learn how to [contribute to or build from the source](./CONTRIBUTING.md).
- Explore the available **[CLI Commands](./docs/cli/commands.md)**.
- If you encounter any issues, review the **[Troubleshooting guide](./docs/troubleshooting.md)**.
- For more comprehensive documentation, see the [full documentation](./docs/index.md).
- Take a look at some [popular tasks](#popular-tasks) for more inspiration.

### Troubleshooting

Head over to the [troubleshooting](docs/troubleshooting.md) guide if you're
having issues.

## Popular tasks

### Explore a new codebase

Start by `cd`ing into an existing or newly-cloned repository and running `gemini`.

```text
> Describe the main pieces of this system's architecture.
```

```text
> What security mechanisms are in place?
```

### Work with your existing code

```text
> Implement a first draft for GitHub issue #123.
```

```text
> Help me migrate this codebase to the latest version of Java. Start with a plan.
```

### Automate your workflows

Use MCP servers to integrate your local system tools with your enterprise collaboration suite.

```text
> Make me a slide deck showing the git history from the last 7 days, grouped by feature and team member.
```

```text
> Make a full-screen web app for a wall display to show our most interacted-with GitHub issues.
```

### Interact with your system

```text
> Convert all the images in this directory to png, and rename them to use dates from the exif data.
```

```text
> Organize my PDF invoices by month of expenditure.
```

### Uninstall

Head over to the [Uninstall](docs/Uninstall.md) guide for uninstallation instructions.

## Terms of Service and Privacy Notice

For details on the terms of service and privacy notice applicable to your use of Gemini CLI, see the [Terms of Service and Privacy Notice](./docs/tos-privacy.md).
