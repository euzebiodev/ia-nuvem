Abaixo está o conteúdo pronto para você salvar como um arquivo .md (por exemplo: conversa-huggingface-runpod-35b.md).

```markdown
# Documento de Referência — Hugging Face, Modelos de Segurança e Execução de Modelos 35B

**Data do documento:** 12/11/2026  
**Cotação usada:** US$ 1 = R$ 5,6507  
**Observação:** Este é um resumo/exportação manual da conversa. O assistente não possui armazenamento persistente nem projeto salvo automaticamente. Guarde este arquivo localmente ou em nuvem própria.

---

## 1. O que é o Hugging Face

O Hugging Face é uma empresa e comunidade de código aberto, frequentemente descrita como o **“GitHub da IA”**. Sua plataforma central é o **Hugging Face Hub**, que hospeda:

- **Modelos de IA** pré-treinados (texto, imagem, áudio etc.)
- **Datasets** públicos e privados
- **Spaces**: demos interativas para testar modelos no navegador
- Bibliotecas open-source, com destaque para **Transformers**

A plataforma democratizou o acesso à IA e é usada por milhões de desenvolvedores, pesquisadores e empresas.

---

## 2. Modelos especializados em segurança no Hugging Face

O ecossistema inclui modelos voltados a cibersegurança, moderação, toxicidade, privacidade e domínios específicos.

### 2.1 Segurança cibernética

- **Uraion Cyber V1.0**: modelo de 35B parâmetros (MoE), focado em segurança defensiva. Analisa código, prova falhas em sandbox, aplica correções e verifica patches.
- **NEMESIS-35B**: modelo tático para operações de cibersegurança.
- **Modelos ofensivos**: projetos como *Offensive-Security-AI-Models* reúnem alternativas especializadas (DeepHat, BugTraceAI, CyberPal etc.).

### 2.2 Guardrails e moderação de conteúdo

- **Llama Guard 4 (Meta)**: multimodal (texto e imagem), 12B parâmetros, detecta conteúdo impróprio na entrada e saída, cobrindo 14 categorias de risco.
- **gpt-oss-safeguard (OpenAI)**: modelos de raciocínio (120B e 20B) que permitem definir a política de segurança em tempo de inferência.
- **FlexGuard-Qwen3-8B**: moderação adaptável, retorna score contínuo de risco (0–100) e categorias de violação.

### 2.3 Toxicidade e classificação de risco

- **Classificadores multilíngues**: exemplo `textdetox/bert-multilingual-toxicity-classifier`, treinado para detectar toxicidade em 15 idiomas.
- **Guard Safety Classifier**: baseado em DeBERTa-v3, faz três previsões simultâneas (seguro, categoria principal e múltiplas categorias de risco).

### 2.4 Privacidade e domínios específicos

- **GLiNER2-Guardrails-PII-Multi**: modelo pequeno (0,3B) que une moderação e detecção de PII em uma única passada, cobrindo 42 tipos de informações sensíveis.
- **MindGuard**: guardrail especializado em segurança em conversas de apoio à saúde mental.

---

## 3. Alternativas mais baratas para rodar um modelo de 35B

Modelos de 35B do tipo **MoE (Mixture of Experts)** ativam apenas uma fração dos parâmetros por token, o que os torna viáveis em hardwares mais modestos, especialmente com quantização.

### 3.1 Opção local

- **GPU usada — RTX 3090 (24 GB)**: melhor custo-benefício. Com quantização Q4, um modelo 35B ocupa cerca de 18 GB de VRAM. Custo entre US$ 600 e US$ 900; desempenho de 40–60 tokens/s.
- **CPU — AMD EPYC 32 núcleos**: alternativa sem GPU. Um modelo 35B pode atingir cerca de 64 tokens/s, com aluguel por volta de US$ 0,20/hora.
- **Apple Silicon**: Macs com 32 GB de memória unificada conseguem rodar versões quantizadas (ex.: Q4 com ~22 GB).

### 3.2 Opção em nuvem

- **RTX 4090 (24 GB)** na Vast.ai: cerca de US$ 0,34/hora para modelo 35B quantizado em INT4.
- **A100 (80 GB)**: a partir de US$ 1,19/hora para precisão total.
- **Quadro RTX 8000 (48 GB)**: a partir de US$ 0,34/hora, roda INT4 com folga.

**Resumo:** para comprar hardware, a **RTX 3090 usada** é a campeã. Para alugar, **CPU na nuvem** ou **RTX 4090** são as melhores opções de baixo custo por hora.

---

## 4. Serviços de nuvem para rodar modelos

### 4.1 Categorias

- **Hiperescaladores (AWS, Google Cloud, Azure)**: ecossistema completo, segurança corporativa, preço por GPU mais alto (ex.: H100 ~US$ 6,88/hora na AWS).
- **Provedores especializados (Lambda, CoreWeave, Nebius, RunPod)**: foco em performance e custo-benefício. Ex.: Lambda H100 ~US$ 3,99/hora; RunPod RTX 4090 a partir de ~US$ 0,34/hora.
- **Plataformas serverless/especializadas (Vast.ai, Together.ai, Fireworks)**: pagamento por segundo ou por token, sem gerenciar servidores.

### 4.2 Modelos de ~35B populares

- **Qwen (Alibaba)**: família Qwen3.5-35B-A3B, MoE que ativa cerca de 3B parâmetros por vez.
- **GLM (Z.ai)**: família GLM-4.7-Flash, 30B parâmetros.
- **Outros**: `decider-35b-a3b`, focado em tomada de decisão.

### 4.3 Modelos sem censura / abliterated

É possível rodar modelos com filtros de segurança removidos (“abliterated”). O Hugging Face abriga esse ecossistema.

- **Índice colaborativo**: `routerhubSI/uncensored-models` no GitHub.
- **Serviços especializados**:
  - **AnonPort**: GPUs em jurisdições offshore, política “no logs”, sem políticas de conteúdo.
  - **Venice.ai**: API com foco em privacidade, acesso a modelos como Gemma 4 Uncensored e GLM 4.7 Flash Heretic, retenção zero.
  - **Imbutus**: foco em segurança ofensiva, modelos como Huihui-CyberStrike-OffSec-35B-abliterated e GLM-5.3-abliterated.

**Aviso:** usar modelos sem censura para pesquisa de malware exige ambiente isolado (sandbox) e finalidade legal/autorizada.

---

## 5. RunPod: acesso remoto, Ollama e persistência

### 5.1 Acesso via VS Code

- O RunPod tem integração oficial com **VS Code Remote-SSH**.
- Configure uma chave SSH na conta RunPod e conecte-se ao Pod como se fosse uma máquina local.
- É possível usar terminal, arquivos e extensões normalmente.

### 5.2 Instalação do modelo

- O tempo depende do modelo e da conexão.
- Modelos quantizados pequenos podem levar cerca de 30 minutos.
- Modelos 35B podem levar mais tempo; use armazenamento persistente para não baixar novamente.

### 5.3 Tipos de armazenamento no RunPod

| Armazenamento | Comportamento |
|---|---|
| **Container Disk** | Efêmero. Apagado ao parar, reiniciar ou terminar o Pod. |
| **Volume Disk** | Sobrevive a “Stop”, mas é apagado ao “Terminate”. |
| **Network Volume** | Persistente. Sobrevive à terminação do Pod. Produto da própria RunPod. |

**Network Volume:**
- Montado em `/workspace`.
- Cobrado por GB/mês: **US$ 0,07/GB/mês** até 1 TB.
- Fica vinculado a um data center específico.
- Para usar o modelo, o Pod deve estar no mesmo data center do volume.

### 5.4 O que o Ollama gera durante a execução

O Ollama grava logs, histórico, cache e arquivos temporários. Esses dados vão para o **Container Disk** por padrão e são apagados ao parar o Pod.

- **Logs**: rotacionados; ~42 MB para mais de 3.000 requisições; limite em torno de 150 MB.
- **Histórico**: mantém apenas as ~100 linhas mais recentes.
- **Runtime**: cenários com histórico e backups ficam em ~1–5 GB.

**Conclusão:** para apenas executar o modelo, não é necessário guardar logs/histórico no Network Volume. O volume serve principalmente para os pesos do modelo.

---

## 6. Tamanho do modelo 35B e espaço necessário

| Quantização | Tamanho aproximado |
|---|---:|
| 4-bit (Q4_K_M) | ~21 GB |
| 5-bit (Q5_K_M) | ~24,7 GB |
| 6-bit (Q6_K) | ~28,5 GB |
| 8-bit (Q8_0) | ~36,9 GB |
| BF16 (precisão total) | ~71,9 GB |

**Recomendação:** um **Network Volume de 50 GB** é suficiente para:
- um modelo 35B em Q4/Q5 (~21–25 GB);
- dados gerados pelo Ollama (~1–5 GB);
- folga para picos temporários ou uma segunda versão.

Custo do volume de 50 GB: **50 × US$ 0,07 = US$ 3,50/mês** (~R$ 19,80).

---

## 7. Simulações de custo no RunPod

### Premissas
- Preços Secure Cloud: **A5000 US$ 0,27/h**, **RTX 3090 US$ 0,50/h**, **RTX 4090 US$ 0,89/h**.
- Network Volume: **50 GB = US$ 3,50/mês**.
- Cotação: **US$ 1 = R$ 5,6507**.

### 7.1 Uso de 2 horas por dia (60 h/mês)

| GPU | Custo GPU | + Armazenamento | Total US$ | Total R$ |
|---|---:|---:|---:|---:|
| RTX A5000 | US$ 16,20 | US$ 3,50 | ~US$ 19,70 | ~R$ 111,30 |
| RTX 3090 | US$ 30,00 | US$ 3,50 | ~US$ 33,50 | ~R$ 189,30 |
| RTX 4090 | US$ 53,40 | US$ 3,50 | ~US$ 56,90 | ~R$ 321,50 |

### 7.2 Uso de 1 hora por dia (30 h/mês)

| GPU | Custo GPU | + Armazenamento | Total US$ | Total R$ |
|---|---:|---:|---:|---:|
| RTX A5000 | US$ 8,10 | US$ 3,50 | ~US$ 11,60 | ~R$ 65,50 |
| RTX 3090 | US$ 15,00 | US$ 3,50 | ~US$ 18,50 | ~R$ 104,50 |
| RTX 4090 | US$ 26,70 | US$ 3,50 | ~US$ 30,20 | ~R$ 170,50 |

**Community Cloud (preços menores):**
- A5000: ~R$ 46,90/mês
- 3090: ~R$ 57,10/mês
- 4090: ~R$ 77,40/mês

### 7.3 Uso de 3 vezes por semana, 1 hora por sessão (~13 h/mês)

| GPU | Custo GPU | + Armazenamento | Total US$ | Total R$ |
|---|---:|---:|---:|---:|
| RTX A5000 | US$ 3,51 | US$ 3,50 | ~US$ 7,01 | ~R$ 39,60 |
| RTX 3090 | US$ 6,50 | US$ 3,50 | ~US$ 10,00 | ~R$ 56,50 |
| RTX 4090 | US$ 11,57 | US$ 3,50 | ~US$ 15,07 | ~R$ 85,20 |

**Community Cloud:**
- A5000: ~R$ 31,50/mês
- 3090: ~R$ 35,90/mês
- 4090: ~R$ 44,80/mês

### 7.4 Se cada sessão durar 2 horas (3x/semana, ~26 h/mês)

| GPU | Total aproximado |
|---|---:|
| A5000 Secure | ~R$ 59,40/mês |
| 3090 Secure | ~R$ 93,20/mês |
| 4090 Secure | ~R$ 150,60/mês |

---

## 8. Velocidade: API DeepSeek via Cline vs modelos locais na nuvem

### 8.1 Geração de tokens

| Opção | Velocidade aproximada |
|---|---|
| API DeepSeek via Cline | 120–150 tok/s em provedores comuns; 178–214 tok/s em otimizados; picos de 233–350 tok/s |
| RTX A5000 (RunPod) | 72–100 tok/s; média ~86 tok/s para Qwen 35B Q4 |
| RTX 3090 (RunPod) | 72–107 tok/s; até ~135 tok/s com ajustes |
| RTX 4090 (RunPod) | 90–120 tok/s; picos de ~157 tok/s |

### 8.2 Latência até o primeiro token (TTFT)

- **Modelos locais no RunPod**: ~350–850 ms, baixa e estável.
- **API DeepSeek via Cline**: variável. Pode ser ~0,76 s em provedores bons, mas passar de 2,5 s em canais como Cline Pass; em contextos longos pode chegar a dezenas de segundos; provedores baratos podem ter TTFT de ~12,41 s.

### 8.3 Recomendação

- **Interatividade e consistência (chat, pequenos ajustes de código):** modelos locais, especialmente RTX 3090/4090.
- **Tarefas longas de geração de código/texto:** API DeepSeek com provedor rápido pode compensar a latência maior.

---

## 9. Serviços de IA sem censura por volta de R$ 50/mês

| Serviço | Preço | Observações |
|---|---:|---|
| **FreedomGPT Starter** | US$ 5/mês (~R$ 28) | Acesso ilimitado a modelos open-source, incluindo “Liberty” sem censura. |
| **SpicyChat** | US$ 5,95/mês (~R$ 34) | Focado em chat adulto/roleplay; não é para codificação. |
| **LoreAPI** | A partir de US$ 2 (~R$ 11) | API compatível com OpenAI, contexto até 1M tokens, sem filtros. Hospedada no Brasil. |
| **Unfiltered AI / API sem restrições** | Pay-per-token: US$ 0,15/1M entrada e US$ 0,50/1M saída | Sem mensalidade fixa; custo depende do uso. |
| **Cleus AI** | US$ 8,95/mês (~R$ 50,60) | Chat e geração de imagens sem censura; confiabilidade limitada. |

**Para uso no VS Code/Cline:**
- **LoreAPI** é a opção mais direta entre as listadas: API compatível com OpenAI, suporte ao Cline, sem filtros e preço baixo.
- **Cleus AI** pode ser possível, mas a integração com VS Code não é bem documentada.
- **SpicyChat** não é recomendado para codificação.

**Alternativa “faça você mesmo”:** alugar servidor barato (ex.: Hetzner US$ 5–10/mês) e rodar modelo open-source sem censura (Dolphin Mistral, Qwen abliterated etc.).

---

## 10. OrcaRouter: custos e acesso

### 10.1 Planos

- **Hacker (gratuito)**: US$ 0/mês, acesso a mais de 200 modelos, 10 chaves de API, zero markup sobre tokens.
- **Team**: US$ 499/mês (valor oficial no site principal), com recursos de equipe, conformidade, chaves ilimitadas e suporte prioritário.
- **Enterprise**: preço sob consulta.

> Alguns sites podem listar planos promocionais ou de parceiros (ex.: ~US$ 49/mês ou Apify a partir de US$ 19/mês). O valor oficial do Team no site principal é US$ 499/mês.

### 10.2 Custo por token — OrcaCyber Zero 1.5

- Entrada: **US$ 3,00/milhão de tokens**
- Saída: **US$ 7,50/milhão de tokens**
- Leitura de cache: **US$ 0,75/milhão de tokens**

O acesso ao OrcaCyber Zero 1.5 é restrito e requer aprovação em um workspace de **Security Research**.

---

## 11. Recomendação final para o cenário do usuário

**Cenário:** uso 3 vezes por semana, ~1 hora por sessão, pesquisa em segurança, modelos 35B, orçamento baixo.

### Opção A — RunPod com RTX 3090
- Custo estimado: **~R$ 35–56/mês** (Community/Secure).
- Vantagens: controle total, liberdade para usar modelos abliterated, latência baixa e estável.
- Desvantagens: exige configuração (Ollama, Network Volume, VS Code Remote SSH) e o modelo pode ter menos conhecimento específico de segurança que um modelo especializado.

### Opção B — OrcaRouter
- Custo variável por token; acesso ao modelo especializado **OrcaCyber Zero 1.5**.
- Vantagens: API compatível com OpenAI, fácil de integrar ao Cline, modelo focado em segurança.
- Desvantagens: acesso restrito/aprovação, custo variável e possível limitação de política de uso.

### Veredito prático
Para começar com segurança e autonomia, **RunPod + RTX 3090** é a aposta mais confiável. Se a profundidade técnica especializada for indispensável, tentar aprovação no **OrcaRouter** em paralelo.

**Aviso legal/ético:** pesquisa com malware deve ocorrer em ambiente isolado (sandbox) e com autorização. Criar ou usar código malicioso contra sistemas sem permissão é crime.

---

## 12. Sobre salvar esta conversa

O assistente **não possui serviço de projeto salvo nem memória persistente** para recuperar esta conversa automaticamente. Para guardar:

1. Salve este arquivo `.md` localmente ou no Google Drive/OneDrive.
2. Se desejar backup visual, use “Salvar como PDF” no navegador.
3. Para organização, cole o conteúdo no Obsidian, Notion ou GitHub.
4. Se a plataforma de chat tiver função nativa de “Exportar conversa” ou “Projetos”, verifique o menu da conversa.

---

**Fim do documento.**
```