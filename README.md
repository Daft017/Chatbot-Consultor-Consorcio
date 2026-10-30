
# 🏠 Chatbot Especializado — Consultor de Consórcio Imobiliário

Chatbot em Python, feito para rodar no Google Colab, que atua como **consultor financeiro e advogado especialista em consórcio imobiliário e documentação de imóvel**. Projeto do **CKP03** da disciplina *Prompt Engineering and Artificial Intelligence* (FIAP, 1º semestre de 2026).

---
Link do Colab: https://colab.research.google.com/drive/15miizuC5gNGBNLlP3T74vUjE7HJi-e6U?usp=sharing
---

## 🎯 O que o chatbot faz

- Explica o consórcio para quem quer comprar um imóvel sem dinheiro à vista e mostra por que começar cedo.
- Orienta sobre situações mais complexas, como a **assunção de dívida com troca de garantia** (transferência de titularidade da carta e da alienação fiduciária).
- Mostra **como a parcela do consórcio é calculada**, passo a passo (crédito + taxa de administração + fundo de reserva, dividido pelo prazo, mais seguro).
- Lembra o que foi dito nos turnos anteriores da conversa.
- Recusa com educação qualquer assunto fora do domínio ("isso não é da minha alçada") e volta ao consórcio.

## 🎭 Personas

O mesmo chatbot tem dois comportamentos distintos, escolhidos por parâmetro. Cada persona tem seus próprios parâmetros de geração:

| Persona | Perfil | `temperature` | `top_p` | Quando usar |
|---|---|---|---|---|
| `consultor` | Léo, consultor financeiro. Tom leve e didático | 0.5 | 0.9 | Dúvidas gerais e iniciantes |
| `advogado` | Dr. Léo, advogado e consultor. Tom leve, mas preciso nos termos jurídicos | 0.3 | 0.8 | Matrícula, alienação, transferência de cota |

A persona do advogado usa valores menores para responder de forma mais precisa e estável. Para criar uma nova persona, basta adicionar uma chave ao dicionário `PERSONAS` no notebook, com `prompt` e `config`.

## 🧩 Como funciona

| Peça | Como foi feita |
|---|---|
| **Modelo** | `gemma4:31b` via Ollama Cloud (sem API paga) |
| **Memória** | Lista `messages` com roles `system`, `user` e `assistant`, enviada inteira a cada turno |
| **System prompt** | Montado por `montar_prompt(usuario, contexto, persona)`: persona + dados do cliente + guardrail + exemplos de comportamento |
| **Guardrail** | Só responde sobre consórcio, financiamento e documentação de imóvel; não inventa números nem promete ganhos; recomenda confirmar com a administradora ou um advogado |
| **Exemplos no prompt** | Compra sem dinheiro à vista, assunção de dívida (com a direção do dinheiro explícita), cálculo de parcela e recusa fora do escopo |
| **Diálogos de teste** | 3 conversas executadas no notebook: caminho feliz, caso difícil e fora do escopo |
| **Modo interativo (bônus)** | Célula opcional para conversar livremente com o bot, ligada pela variável `MODO_INTERATIVO` |

## 📓 Estrutura do notebook

O notebook tem três células, nesta ordem:

1. **Texto (markdown):** explica domínio, personas, tom, guardrail e decisões técnicas.
2. **Código principal:** configuração, personas, guardrail, exemplos, template de prompt, chamada ao modelo e os 3 diálogos de teste.
3. **Código opcional (conversa livre):** permite digitar perguntas e conversar com o bot.

## ▶️ Como executar

1. Abra o notebook no Google Colab.
2. Crie uma chave de API em [ollama.com/settings/keys](https://ollama.com/settings/keys).
3. No Colab, abra o ícone de chave 🔑 (**Secrets**) na barra lateral e adicione um segredo chamado exatamente `OLLAMA_API_KEY`, com o valor da sua chave.
4. Ative a opção **"Acesso ao notebook"** desse segredo.
5. Vá em **Ambiente de execução → Executar tudo**.

A chave é lida com `userdata.get('OLLAMA_API_KEY')` e **nunca fica escrita no código**.

### 💬 Conversando livremente com o bot (opcional)

Na terceira célula, a variável `MODO_INTERATIVO` vem como `False`, para o **Executar tudo** não ficar esperando alguém digitar. Para conversar:

1. Rode primeiro a célula principal.
2. Na terceira célula, troque para `MODO_INTERATIVO = True` e rode só ela.
3. Digite suas perguntas na caixa que aparece e use `sair` para encerrar.
4. Para falar com o advogado, troque `persona="consultor"` por `persona="advogado"` na chamada de `conversar(...)`.

## 💬 Diálogos de exemplo

| # | Cenário | Persona | O que mostra |
|---|---|---|---|
| 1 | Quer comprar a casa própria sem dinheiro à vista | `consultor` | Explicação do consórcio e memória do contexto |
| 2 | Quer quitar a carta de consórcio pagando menos | `advogado` | Assunção de dívida com troca de garantia |
| 3 | Pede uma receita de bolo e tenta burlar as regras | `consultor` | Guardrail e retorno ao tema |

## 📁 Estrutura do repositório

```
├── README.md
└── ChatBotConsorcioV0.4.ipynb   # notebook com a explicação, o código e os diálogos
```

## ⚠️ Aviso

Este é um projeto **educacional**. As respostas do chatbot não substituem a orientação de um advogado, de um consultor financeiro ou da administradora do consórcio. Regras, taxas, prazos e valores de exemplo (como o cálculo de parcela) são ilustrativos e variam conforme o contrato e a administradora, e devem ser sempre confirmados antes de qualquer decisão.

## 👥 Equipe

 - Gabriel de Paula Santa Izabel
 - Lucas Jorge Ferreira
 - Victor Hugo Astorino Barra Mansa

Disciplina: Prompt Engineering and Artificial Intelligence · FIAP · CC 2026
