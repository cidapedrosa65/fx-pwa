# MCP do CapCut

Este repositório tem um `.mcp.json` que registra o servidor MCP `capcut` no Claude Code.
Ele usa o [VectCutAPI](https://github.com/sun-guannan/VectCutAPI) (código aberto, Apache-2.0,
não oficial da CapCut/ByteDance), que monta rascunhos (drafts) do CapCut: vídeo, áudio,
texto, legendas, efeitos e transições.

O CapCut é um app de desktop, então o servidor roda **no seu computador**, não numa sessão na nuvem.

## Instalação (uma vez)

Requisitos: Python 3.10+, FFmpeg e CapCut desktop.

```bash
git clone https://github.com/sun-guannan/VectCutAPI.git
cd VectCutAPI
python3 -m venv venv-capcut
source venv-capcut/bin/activate        # Windows: venv-capcut\Scripts\activate
pip install -r requirements.txt
pip install -r requirements-mcp.txt
cp config.json.example config.json     # em config.json, draft_profile: "capcut_legacy"
```

Aponte a variável `VECTCUT_DIR` para essa pasta (ex.: no `~/.zshrc` ou `~/.bashrc`):

```bash
export VECTCUT_DIR="$HOME/VectCutAPI"
```

Se você usa o venv, troque `"command": "python3"` no `.mcp.json` pelo Python do venv
(ex.: `${VECTCUT_DIR}/venv-capcut/bin/python`).

## Uso

1. Abra o Claude Code nesta pasta: `claude`. Aprove o servidor `capcut` quando ele perguntar.
2. Confira com `/mcp` que o `capcut` está conectado.
3. Peça coisas como: "crie um rascunho 9:16, adicione omundoaqui.png por 3s com o texto X e salve".
4. O `save_draft` cria uma pasta `dfd_...`. Copie essa pasta para a pasta de rascunhos do CapCut:
   - macOS: `~/Movies/CapCut/User Data/Projects/com.lveditor.draft/`
   - Windows: `%LOCALAPPDATA%\CapCut\User Data\Projects\com.lveditor.draft\`
5. Abra o CapCut: o rascunho aparece na lista de projetos.

## Alternativa

[JmsLdrn/capcut-mcp](https://github.com/JmsLdrn/capcut-mcp) (Node 18+) edita os rascunhos do CapCut
direto, sem copiar pastas. É bem mais novo (um commit só), então faça backup dos projetos antes de usar.
