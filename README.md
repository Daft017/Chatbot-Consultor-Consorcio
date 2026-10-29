# 🏠 Chatbot Especializado — Consultor de Consórcio Imobiliário

Chatbot em Python, feito para rodar no Google Colab, que atua como **consultor financeiro e advogado especialista em consórcio imobiliário e documentação de imóvel**. Projeto do **CKP03** da disciplina *Prompt Engineering and Artificial Intelligence* (FIAP, 1º semestre de 2026).

> 🔗 **Notebook no Colab:** `[COLE AQUI O LINK PÚBLICO DO COLAB]`

---

## 🎯 O que o chatbot faz

- Explica o consórcio para quem quer comprar um imóvel sem dinheiro à vista e mostra por que começar cedo.
- Orienta sobre situações mais complexas, como a **assunção de dívida com troca de garantia** (transferência de titularidade da carta e da alienação fiduciária).
- Lembra o que foi dito nos turnos anteriores da conversa.
- Recusa com educação qualquer assunto fora do domínio ("isso não é da minha alçada") e volta ao consórcio.

## 🎭 Personas

O mesmo chatbot tem dois comportamentos distintos, escolhidos por parâmetro:

| Persona | Perfil | Quando usar |
|---|---|---|
| `consultor` | Léo, consultor financeiro. Tom leve e didático | Dúvidas gerais e iniciantes |
| `advogado` | Dr. Léo, advogado e consultor. Tom leve, mas preciso nos termos jurídicos | Matrícula, alienação, transferência de cota |

Para criar uma nova persona, basta adicionar uma chave ao dicionário `PERSONAS` no notebook.

## 🧩 Como funciona

| Peça | Como foi feita |
|---|---|
| **Modelo** | `gemma4:31b` via Ollama Cloud (sem API paga) |
| **Memória** | Lista `messages` com roles `system`, `user` e `assistant`, enviada inteira a cada turno |
| **System prompt** | Montado por `montar_prompt(usuario, contexto, persona)`: persona + dados do cliente + guardrail + exemplos de comportamento |
| **Guardrail** | Só responde sobre consórcio, financiamento e documentação de imóvel; não inventa números nem promete ganhos; recomenda confirmar com a administradora ou um advogado |
| **Diálogos de teste** | 3 conversas executadas no notebook: caminho feliz, caso difícil e fora do escopo |
| **Pesquisa web (opcional)** | Ferramenta `pesquisar_web`, ligada ou desligada pela variável `USAR_PESQUISA` |

## ▶️ Como executar

1. Abra o notebook no Google Colab.
2. Crie uma chave de API em [ollama.com/settings/keys](https://ollama.com/settings/keys).
3. No Colab, abra o ícone de chave 🔑 (**Secrets**) na barra lateral e adicione um segredo chamado exatamente `OLLAMA_API_KEY`, com o valor da sua chave.
4. Ative a opção **"Acesso ao notebook"** desse segredo.
5. Vá em **Ambiente de execução → Executar tudo**.

A chave é lida com `userdata.get('OLLAMA_API_KEY')` e **nunca fica escrita no código**.

## 💬 Diálogos de exemplo

| # | Cenário | Persona | O que mostra |
|---|---|---|---|
| 1 | Quer comprar a casa própria sem dinheiro à vista | `consultor` | Explicação do consórcio e memória do contexto |
| 2 | Quer quitar a carta de consórcio pagando menos | `advogado` | Assunção de dívida com troca de garantia |
| 3 | Pede uma receita de bolo e tenta burlar as regras | `consultor` | Guardrail e retorno ao tema |

## 📁 Estrutura do repositório

```
├── README.md
└── chatbot_consorcio.ipynb   # notebook com a explicação, o código e os diálogos
```

## ⚠️ Aviso

Este é um projeto **educacional**. As respostas do chatbot não substituem a orientação de um advogado, de um consultor financeiro ou da administradora do consórcio. Regras, taxas e prazos variam conforme o contrato e a administradora, e devem ser sempre confirmados antes de qualquer decisão.

## 👥 Equipe

`Gabriel de Paula Santa Izabel
Victor Hugo Astorino Barra Mansa
João pedro de Francisco Godoy
Lucas Jorge Ferreira`

Disciplina: Prompt Engineering and Artificial Intelligence · FIAP · CC 2026
