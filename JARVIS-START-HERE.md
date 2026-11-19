# Jarvis local setup

This workspace contains the official [OpenJarvis](https://github.com/open-jarvis/OpenJarvis) source. Recommended path: start with local chat, confirm it works, then add integrations only when you want them.

## 1. Install the project dependencies

From this directory, install [uv](https://docs.astral.sh/uv/) if it is not already installed, then run:

```bash
uv sync
```

This prepares the project environment in `.venv`. The project requires Python 3.11–3.13.

## 2. Add a local inference backend

OpenJarvis needs an inference backend. For a straightforward local setup, install [Ollama](https://ollama.com/) using its official Linux instructions, start its service, and download a model that fits your machine. The upstream example uses `qwen3.5:4b`:

```bash
ollama pull qwen3.5:4b
```

If your computer has limited memory, choose a smaller model; larger models need more RAM/VRAM and disk space.

## 3. Initialize local chat

```bash
uv run jarvis init --preset chat-simple
uv run jarvis
```

The `chat-simple` preset uses the local Ollama engine and a simple chat agent. If you already have a Jarvis configuration you want to preserve, inspect it before using any `--force` option; that option replaces the generated configuration.

## Optional next steps

- **Browser UI:** install Node.js 22 or newer, then run `uv run jarvis gui` from this source checkout.
- **Daily email/calendar briefing:** first review the permissions requested by `uv run jarvis connect gdrive`. This connects Google services through one OAuth flow. Then follow the upstream morning-digest guide for your platform.
- **Cloud models or ElevenLabs voice:** configure them only after reviewing their current provider documentation, privacy terms, and usage limits. Do not put API keys in chat or commit them to this repository. OpenJarvis does not automatically load `.env` files in every launch path; use the documented environment/configuration method for the chosen integration.

## References

- [Upstream installation guide](https://open-jarvis.github.io/OpenJarvis/getting-started/install/)
- [Upstream quickstart](https://open-jarvis.github.io/OpenJarvis/getting-started/quickstart/)
- [Chat-simple preset](configs/openjarvis/examples/chat-simple.toml)
