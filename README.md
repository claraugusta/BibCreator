# AgenteExtrator

Pipeline de extração de metadados bibliográficos de papers acadêmicos em PDF, construído com **CrewAI** e **NVIDIA NIM** (Llama 3.1 70B Instruct).

Dois agentes trabajam em sequência:

1. **Team Archivist** — busca um arquivo na pasta `data/`, resolve nomes parciais/typos, e extrai o texto do PDF.
2. **Academic Metadata Extractor** — analisa o texto bruto e gera um arquivo .bib estruturado com campos como título, autores, ano, DOI, periódico, etc.

## Pré-requisitos

- Python 3.12+
- [uv](https://docs.astral.sh/uv/) (gerenciador de pacotes)
- Chave de API da NVIDIA NIM ([obter aqui](https://build.nvidia.com/))

## Instalação

```bash
# Clonar o repositório
git clone https://github.com/claraugusta/BibCreator.git

# Instalar dependências
pip install -r requirements.txt

uv init
uv add "crewai[litellm]"
```

## Configuração

Crie um arquivo `.env` na raiz do projeto:

```
NVIDIA_API_KEY=sua_chave_aqui
```

## Uso

1. Coloque os PDFs desejados na pasta `data/`.
2. Abra o notebook `agent.ipynb` e execute todas as células.
3. Na última célula, substitua `'langgraph paper'` pelo nome (ou parte do nome) do arquivo que deseja processar:

```python
result = crew.kickoff(inputs={"filename": "langgraph paper"})
```

O resultado é um JSON com a entrada bibliográfica estruturada.

## Estrutura do projeto

```
AgenteExtrator/
├── agent.ipynb          # Notebook principal com o pipeline completo
├── data/                # Pasta onde os PDFs devem ser colocados
├── main.py              # Script placeholder
├── pyproject.toml       # Configuração do projeto (uv)
├── requirements.txt     # Dependências
└── .env                 # Chave de API (não versionar)
```

## Dependências principais

| Pacote | Uso |
|--------|-----|
| `crewai` | Framework de agentes |
| `crewai-tools` | Ferramentas prontas (DirectoryReadTool) |
| `pypdf` | Extração de texto de PDFs |
| `pydantic` | Schema estruturado de saída |
| `langchain-nvidia-ai-endpoints` | Integração com NVIDIA NIM |
