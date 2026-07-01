# Terraform Associate (004) - Certification Journey 🚀

Este repositório documenta minha jornada de estudos e preparação para a certificação **Hashicorp Certified: Terraform Associate (004)**, concluída com sucesso em maio de 2026.

## 📌 Sobre a Certificação
A certificação valida o conhecimento em Infraestrutura como Código (IaC), o ecossistema Terraform, e especificamente as funcionalidades da versão 004, como:

- **Custom Validation Conditions** e **Check Blocks**.
- Gerenciamento avançado de estado e **Drift Detection**.
- Governança e organização no **HCP Terraform (Workspaces & Projects)**.

## 📂 Estrutura do Repositório

- `/study-guides`: Resumos teóricos detalhados em Português e Inglês.
- `/flashcards`: Conjuntos de flashcards para revisão rápida.
- `/pratices-tests`: Questões e simulados de prática.

## 🛠️ Ferramentas Utilizadas

- Terraform CLI (v1.x)
- HCP Terraform (Cloud)
- AWS (provedor de infraestrutura para labs)
- NotebookLM (suporte para análise de fontes e geração de simulados)

## 📘 Exemplo de Conteúdo

### Mock Questions - Terraform Associate 004

#### Q1: State Management
**Pergunta:** O que acontece com a infraestrutura real ao executar `terraform state rm <resource_address>`?

**Resposta:** O recurso permanece ativo na nuvem. O Terraform apenas remove a entrada correspondente do arquivo de estado, deixando de gerenciá-lo.

#### Q2: HCP Terraform Hierarchy
**Pergunta:** Qual a diferença entre Workspaces e Projects no HCP Terraform?

**Resposta:** **Workspaces** são as unidades técnicas que gerenciam um arquivo de estado individual. **Projects** são contêineres organizacionais que agrupam múltiplos workspaces para melhor governança e controle de acesso.

#### Q3: Terraform Import
**Pergunta:** O comando `terraform import` gera automaticamente o código de configuração (.tf)?

**Resposta:** Não. Ele apenas mapeia o recurso existente para o estado. O usuário deve escrever manualmente o bloco de configuração correspondente.
