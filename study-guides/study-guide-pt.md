# Guia de Estudo Técnico: Certificação HashiCorp Certified Terraform Associate (004)

Como engenheiro DevOps, sei que a certificação não é apenas sobre decorar comandos, mas entender o ciclo de vida da infraestrutura e evitar desastres em produção. Este guia foca na versão 004 do exame, que traz mudanças significativas em relação à anterior.

---

## 1. Visão Geral do Exame Terraform Associate (004)

O exame valida o domínio do Terraform Community Edition e do HCP Terraform em fluxos produtivos.

- **Versão alvo:** O exame testa conhecimentos baseados no Terraform 1.12.
- **Duração:** 60 minutos.
- **Formato:** Questões de múltipla escolha, múltipla seleção e verdadeiro/falso.
- **Mudança importante:** Questões de tipo "preencher lacunas" foram removidas na versão 004.
- **Plataforma:** Realizado via Certiverse.
- **Validade:** 2 anos.

> **Alerta de versão:** O exame 003 foi aposentado em janeiro de 2026. A versão 004 é agora a única disponível. Se você estudou para a 003, foque nas seções de "Novas Funcionalidades" deste guia.

---

## 2. Fundamentos de Infraestrutura como Código (IaC) e Terraform

IaC é a prática de gerenciar infraestrutura através de arquivos de configuração, garantindo automação, consistência e rastreabilidade via controle de versão (Git). O Terraform se destaca por ser service-agnostic, gerenciando fluxos híbridos e multi-cloud sob uma única linguagem (HCL).

| Característica | Resource Blocks | Data Source Blocks |
|---|---|---|
| Objetivo | Criar e gerenciar novos recursos | Consultar informações de infraestrutura existente |
| Dono do ciclo de vida | O Terraform (cria, altera, destrói) | Externo (Terraform apenas lê os dados) |
| Uso comum | Instâncias EC2, bancos RDS | Consultar um ID de VPC ou uma AMI atual |

---

## 3. Fluxo de Trabalho Principal (Core Workflow)

O workflow padrão é: **Write -> Plan -> Apply**.

- `terraform init`: Prepara o diretório. Cria a pasta oculta `.terraform/`, inicializa o backend, instala módulos filhos e baixa os providers.
  - Use `terraform init -upgrade` para forçar a atualização de plugins para versões mais recentes.
- `terraform validate`: Verificação estática e sintática. É executado localmente e não acessa APIs remotas ou serviços de nuvem.
- `terraform plan`: Gera um plano de execução. Por padrão, o plan realiza um refresh do estado, o que significa que ele pode atualizar o arquivo de estado (`.tfstate`) ao ler a realidade da infraestrutura, embora não altere os recursos reais.
- `terraform apply`: Aplica as mudanças. Atualiza o estado e a infraestrutura. A flag `-auto-approve` ignora a confirmação interativa.
- `terraform destroy`: Remove totalmente os recursos gerenciados pelo estado atual.
- `terraform fmt`: Ajusta o estilo e a indentação para consistência do time.

---

## 4. Gerenciamento de Estado (State Management)

O estado (`terraform.tfstate`) é o mapeamento entre seu código e a realidade na nuvem.

### Conceitos e Backends

- **Local vs remoto:** O backend local é para testes. Em produção, usamos backends remotos (S3, HCP Terraform) para permitir colaboração e garantir state locking, impedindo que dois engenheiros corrompam o arquivo ao rodar comandos simultâneos.

- **Comandos de inspeção:**
  - `terraform state list`: Lista os recursos no estado.
  - `terraform state show`: Detalha um recurso específico.
  - `terraform state rm`: Remove o recurso do estado. **CUIDADO:** O recurso físico continua existindo na nuvem. Se você rodar um `apply` logo após, o Terraform poderá tentar recriar o recurso, pois o código ainda o define, mas o estado o esqueceu.

### Drift e sincronização

Para detectar mudanças manuais feitas fora do Terraform (drift), usamos `terraform apply -refresh-only`. Ele sincroniza o arquivo de estado com a realidade sem modificar a infraestrutura.

---

## 5. Variáveis, Outputs e Tipos Complexos

- **Variables (input):** Argumentos para o módulo. Prática recomendada: usar arquivos `.tfvars`.
- **Outputs:** Expõem dados (por exemplo, endereço IP). Para ver outputs de módulos filhos no CLI, eles devem ser explicitamente passados para o módulo raiz.
- **Tipos:** Primitivos (`string`, `number`, `boolean`) e complexos (`list`, `set`, `map`, `object`).
- **Aviso de segurança:** `sensitive = true` apenas mascara o valor no console e logs. O segredo continuará em texto claro no arquivo de estado. Proteja seu backend com criptografia ou uso de HCP Terraform.

---

## 6. Uso de Módulos

Módulos são contêineres para reutilização de código.

- **Escopo:** Variáveis de entrada são os argumentos do módulo; outputs são como ele retorna dados.
- **Fontes:** Podem ser locais (caminho de pasta) ou remotos (Terraform Registry, Git).
- **Módulos filhos:** São instalados durante o `terraform init`.

---

## 7. Novas Funcionalidades e Diferenciais (Versão 004)

Esses itens são críticos para quem vem da versão 003:

- **Custom Validation Conditions:** Blocos `validation` dentro de variáveis criam guardrails, impedindo que valores inválidos iniciem o deploy.
- **Check Blocks:** Validam a infraestrutura após a execução do `apply`. Diferente do `validate`, eles não interrompem o fluxo se falharem; apenas alertam sobre o status de saúde.
- **Ephemeral Values e write-only arguments:** Novos recursos de segurança para lidar com dados sensíveis que não devem ser persistidos no estado.
- **Dependências explícitas:** Uso do `depends_on`.
- **Lifecycle rules:** `create_before_destroy` evita downtime ao criar um recurso substituto antes de remover o antigo.

---

## 8. Manutenção, Troubleshooting e HCP Terraform

### Troubleshooting

- **Logging:** Use `TF_LOG` (TRACE, DEBUG, INFO, WARN, ERROR) e `TF_LOG_PATH` para depurar problemas de API.
- **Importação:** `terraform import` mapeia um recurso real ao estado, mas não escreve o código HCL automaticamente. Você deve escrever manualmente o bloco `resource` correspondente.

### HCP Terraform (Terraform Cloud)

Plataforma SaaS para governança:

- **Workspaces e projetos:** Organização de times.
- **Camadas (tiers):** O plano Business oferece agentes privados e Single Sign-On (SSO).
- **Governança:** Sentinel e OPA atuam como filtros entre o plan e o apply.

---

## 9. Dicas Práticas para o Dia do Exame

1. Elimine comandos inexistentes. O exame costuma inventar alternativas falsas.
2. Diferencie os arquivos: `.terraform.lock.hcl` é para versões de plugins; `terraform.tfstate` é para a realidade da infraestrutura.
3. Atenção aos enunciados: questões que pedem DUAS alternativas são armadilhas comuns.
4. Em um cenário `state rm`, o Terraform apenas "esquece" o recurso; o recurso físico permanece intacto até ser deletado manualmente ou pela configuração.

---

## 10. Recursos de Estudo Recomendados

- Documentação oficial: HashiCorp Learning Path (004).
- Simulados profissionais: Bryan Krausen (Udemy) atualizado para 004.
- Livro: _Terraform: Up & Running_ (Yevgeniy Brikman).
- Prática: repositórios no GitHub e labs da LinuxTips.

