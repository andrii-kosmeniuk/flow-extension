# UNIQA Conversion Coach

Chrome extension + Coach API that shows conversion-coaching prompts on the live UNIQA health insurance calculator.

This README is only for judges who want to run the project and see the demo.

## What You Need

- Node.js 22+ and npm
- Docker or Docker Desktop
- Google Chrome
- Ollama, for the local LLM model

## Run The Local Demo

Set up the project:

```bash
git clone <repo-url>
cd github_version
cp .env.example .env
npm install
```

Start Ollama and pull the local model:

```bash
ollama serve
ollama pull qwen2.5:3b-instruct
```

Keep Ollama running. The default `.env.example` is already configured to use:

```text
LLM_PROVIDER=local
LLM_API_URL=http://localhost:11434/v1/chat/completions
LLM_MODEL=qwen2.5:3b-instruct
```

Start the local database and Coach API:

```bash
npm run db:up
npm run db:migrate
npm run dev:coach-api
```

Keep this terminal open. The API should run at:

```text
http://127.0.0.1:8787
```

In another terminal, build the Chrome extension:

```bash
npm run build:extension
```

Load the extension in Chrome:

1. Open `chrome://extensions`.
2. Enable **Developer mode**.
3. Click **Load unpacked**.
4. Select the `extension/dist` folder.

Open the UNIQA calculator:

```text
https://www.uniqa.at/krankenversicherung/rechner
```

To see the coach popups, walk through a Start or Optimal path with:

- Private doctor
- Myself only

The extension should detect the current funnel step and show coaching prompts while the local Coach API is running.

## If The Local Setup Is Not Working

If the database or local API does not work, use the deployed Coach API instead.

In `.env`, set:

```text
VITE_COACH_API_ORIGIN=https://coach-api-42il2.ondigitalocean.app/
```

Then rebuild the extension:

```bash
npm install
npm run build:extension
```

Load `extension/dist` in Chrome again and open the UNIQA calculator. The extension will call the deployed API instead of `http://127.0.0.1:8787`.

## Submission Materials

The final report, hypotheses, demo guide, and precomputed results are in:

```text
submissions/4Thrives/
```
