# Plano de Estudos: Terraform Associate (004) — 6 Semanas

Breve: Plano de 6 semanas para cobrir os objetivos do exame Terraform Associate.


- OBS: O Plano é sugerido para quem tem conhecimento basicos e já trabalha como o Terraform no dia a dia.

## Materias de estudo
**Links**
- https://developer.hashicorp.com/terraform/tutorials/certification-004/associate-study-004
- https://developer.hashicorp.com/terraform/tutorials/certification-004/associate-review-004
- https://www.udemy.com/course/terraform-associate-004-practice-exams/?couponCode=MT260629G1
- https://www.udemy.com/course/terraform-beginner-to-advanced/

## Orientação

- Siga as semanas de acordo com o guia de "study e review" da Hashicorp, da Semana 1 até 5.
- Revise os conteúdo assistindo o curso do "terraform-beginner-to-advanced" na Udemy
- Realize os simulados do "terraform-beginner-to-advanced" na Udemy, tenha um notas acima de 85% para se adaptar a prova.
- Utilize o NotebookLM para gerar fontes sobre o "Terraform Associate (004)" e depois peça para ele gerar Resumos, Flashcards, Quiz sobre a prova. Aconselhável você solicitar em Português e Inglês.


## Semana 1 — Fundamentos, IaC e Provedores (Objetivos 1 e 2)

Foco: Por que usar Terraform e como ele se conecta às nuvens.

**Tópicos oficiais**
- Vantagens do IaC: reutilização, automação e consistência.
- Fluxos agnósticos: multi-cloud e nuvem híbrida.
- Provedores: requisitos de versão, bloco `provider` e o arquivo de lock (`.terraform.lock.hcl`).

**Termos em inglês**: `Agnostic`, `Multi-cloud`, `Dependency lock`, `Version constraints`.

## Semana 2 — O Fluxo de Trabalho Core (Objetivo 3)

Foco: O ciclo de vida dos comandos CLI.

**Tópicos oficiais**
- `terraform init`: inicialização de backends, provedores e módulos.
- `terraform validate` vs `terraform fmt`: checar sintaxe vs formatar estilo.
- `terraform plan`, `terraform apply` e `terraform destroy`: ciclo completo.
- Entender o Resource Graph (ordem de criação de recursos).

**Termos em inglês**: `Execution plan`, `Formatting`, `Validation`, `Working directory`.

## Semana 3 — Variáveis, Tipos Complexos e Funções (Objetivo 4)

Foco: Deixar o código parametrizável e reutilizável.

**Tópicos oficiais**
- Diferença entre blocos `resource` (criar) e `data` (consultar).
- Tipos complexos: `list`, `map`, `object`, `set`.
- Segurança: gerenciamento de dados sensíveis e integração com Vault.
- Expressões dinâmicas e funções integradas; uso de blocos dinâmicos.

**Termos em inglês**: `Data sources`, `Output variables`, `Sensitive data`, `Built-in functions`.

## Semana 4 — Módulos e Gestão de Estado (Objetivos 5 e 6)

Foco: Organização do código e a "memória" do Terraform.

**Tópicos oficiais**
- Escopo de variáveis em módulos: variáveis de entrada e saída.
- Origem dos módulos: Registry, Git, local.
- State: backends locais vs remotos; state locking.
- Drift: detecção e tratamento de mudanças manuais fora do código.

**Termos em inglês**: `Module scope`, `Remote state`, `State locking`, `Resource drift`.

## Semana 5 — Manutenção e HCP Terraform (Objetivos 7 e 8)

Foco: Comandos avançados, manutenção e plataforma HCP Terraform.

**Tópicos oficiais**
- `terraform import`: trazer recursos existentes para o state.
- Depuração: uso de logs (`TF_LOG`) e diagnóstico de falhas.
- HCP Terraform / Terraform Cloud: projetos, workspaces, governança (Sentinel/OPA) e detecção de drift.
- Diferença entre Workspaces da CLI e Workspaces do HCP Terraform.

**Termos em inglês**: `Verbose logging`, `Governance`, `Policy enforcement`, `Sentinel`.

## Semana 6 — Revisão Final e Estratégia de Prova

Foco: Simulação do exame e reforço de leitura rápida em inglês.

**Atividades recomendadas**
- Revisar as questões de exemplo (Sample Questions) e cronometrar as tentativas.
- Revisitar objetivos com maior dificuldade.
- Treinar interpretação de enunciados com foco em "best practice" e redução de esforço.

> **Dica de estudo (inglês):** A documentação HashiCorp é bem estruturada. Use uma extensão de tradução para entender conceitos, mas memorize os nomes de comandos e parâmetros em inglês — o exame cobra termos e palavras-chave.

---
