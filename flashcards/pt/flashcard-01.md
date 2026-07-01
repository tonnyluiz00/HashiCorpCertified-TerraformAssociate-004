# Flashcards PT - Conjunto 01

## Flashcard 01
**Pergunta:** O que caracteriza a Infraestrutura como Código (IaC)?

**Resposta:** O gerenciamento e provisionamento de infraestrutura através de arquivos de configuração legíveis por máquina.

---

## Flashcard 02
**Pergunta:** Qual é a principal vantagem de utilizar padrões de IaC em vez de provisionamento manual via interface gráfica?

**Resposta:** Redução do risco de erro humano e facilitação do versionamento e compartilhamento de configurações.

---

## Flashcard 03
**Pergunta:** Como o Terraform gerencia fluxos de trabalho que envolvem múltiplas nuvens ou nuvens híbridas?

**Resposta:** Através do uso de provedores (`providers`) que abstraem as APIs de diferentes serviços.

---

## Flashcard 04
**Pergunta:** Qual comando deve ser executado primeiro em um diretório de trabalho antes de outras operações?

**Resposta:** `terraform init`

---

## Flashcard 05
**Pergunta:** O comando `terraform init` realiza quais tarefas principais?

**Resposta:** Inicializa o backend, baixa os plugins dos provedores e instala módulos dependentes.

---

## Flashcard 06
**Pergunta:** Qual arquivo é gerado para registrar as versões exatas e os checksums dos provedores instalados?

**Resposta:** `.terraform.lock.hcl`

---

## Flashcard 07
**Pergunta:** O que os `providers` representam no ecossistema do Terraform?

**Resposta:** Plugins que permitem ao Terraform interagir com APIs de provedores de nuvem e outros serviços.

---

## Flashcard 08
**Pergunta:** Onde o Terraform busca por provedores se nenhum endereço privado for especificado?

**Resposta:** Terraform Registry público.

---

## Flashcard 09
**Pergunta:** Como o Terraform utiliza o arquivo de estado (`state file`)?

**Resposta:** Para mapear os recursos do mundo real para a sua configuração e rastrear metadados.

---

## Flashcard 10
**Pergunta:** Qual é a finalidade do comando `terraform validate`?

**Resposta:** Verificar se a sintaxe da configuração e os argumentos internos estão corretos sem acessar serviços remotos.

---

## Flashcard 11
**Pergunta:** O que o comando `terraform plan` exibe ao usuário?

**Resposta:** Um plano de execução detalhando as alterações que serão feitas na infraestrutura para atingir o estado desejado.

---

## Flashcard 12
**Pergunta:** Qual comando aplica as alterações planejadas na infraestrutura?

**Resposta:** `terraform apply`

---

## Flashcard 13
**Pergunta:** O comando `terraform apply` atualiza qual arquivo após a conclusão bem-sucedida?

**Resposta:** O arquivo de estado (`state file`).

---

## Flashcard 14
**Pergunta:** Qual comando remove permanentemente todos os recursos gerenciados por um arquivo de estado?

**Resposta:** `terraform destroy`

---

## Flashcard 15
**Pergunta:** Para que serve o comando `terraform fmt`?

**Resposta:** Reformatar os arquivos de configuração para seguir as convenções de estilo do Terraform.

---

## Flashcard 16
**Pergunta:** Qual é a diferença entre um bloco `resource` e um bloco `data`?

**Resposta:** `resource` gerencia a criação de infraestrutura; `data` lê informações de recursos que já existem.

---

## Flashcard 17
**Pergunta:** Como se faz uma referência a um atributo de um recurso em outro bloco?

**Resposta:** Utilizando a sintaxe `<TIPO_DO_RECURSO>.<NOME_DO_RECURSO>.<ATRIBUTO>`.

---

## Flashcard 18
**Pergunta:** Qual é o propósito das `input variables` no Terraform?

**Resposta:** Permitir a parametrização de configurações para torná-las reutilizáveis sem alterar o código principal.

---

## Flashcard 19
**Pergunta:** Onde são definidos os valores que o Terraform deve exibir após a execução de um `apply`?

**Resposta:** No bloco `output`.

---

## Flashcard 20
**Pergunta:** O que acontece se uma variável for declarada com `sensitive = true`?

**Resposta:** O Terraform mascara o seu valor nas saídas do console e logs da CLI.

---

## Flashcard 21
**Pergunta:** A marcação `sensitive = true` remove o valor do arquivo de estado?

**Resposta:** Não, o valor ainda permanece em texto claro dentro do arquivo de estado.

---

## Flashcard 22
**Pergunta:** Qual meta-argumento é usado para criar dependências explícitas entre recursos?

**Resposta:** `depends_on`

---

## Flashcard 23
**Pergunta:** O que é um `Terraform module`?

**Resposta:** Um conjunto de arquivos de configuração em um único diretório usados para organizar e reutilizar código.

---

## Flashcard 24
**Pergunta:** Um módulo filho tem acesso automático às variáveis do módulo pai?

**Resposta:** Não, as variáveis devem ser passadas explicitamente como argumentos na chamada do módulo.

---

## Flashcard 25
**Pergunta:** O que o comando `terraform state rm` faz com um recurso?

**Resposta:** Remove o recurso do arquivo de estado, mas não o destrói na infraestrutura real.

---

## Flashcard 26
**Pergunta:** Qual é a função do `state locking`?

**Resposta:** Impedir que múltiplos usuários executem operações de escrita simultâneas no mesmo arquivo de estado.

---

## Flashcard 27
**Pergunta:** Qual comando traz um recurso já existente para o gerenciamento do Terraform?

**Resposta:** `terraform import`

---

## Flashcard 28
**Pergunta:** O comando `terraform import` gera automaticamente o código de configuração `.tf`?

**Resposta:** Não, o usuário deve escrever manualmente o bloco de recurso correspondente no código.

---

## Flashcard 29
**Pergunta:** Qual variável de ambiente controla o nível de detalhamento dos logs do Terraform?

**Resposta:** `TF_LOG`

---

## Flashcard 30
**Pergunta:** Quais são os 5 níveis possíveis para a variável `TF_LOG`?

**Resposta:** `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`

---

## Flashcard 31
**Pergunta:** O que é o HCP Terraform?

**Resposta:** Uma plataforma SaaS da HashiCorp para colaboração, armazenamento de estado remoto e execução gerenciada do Terraform.

---

## Flashcard 32
**Pergunta:** O que são `run triggers` no HCP Terraform?

**Resposta:** Mecanismos que iniciam um novo plano em um workspace quando outro workspace completa uma alteração.

---

## Flashcard 33
**Pergunta:** Na versão 004, qual bloco permite monitorar a conformidade da infraestrutura após o provisionamento?

**Resposta:** `check`

---

## Flashcard 34
**Pergunta:** Para que serve o bloco `moved` introduzido em versões recentes do Terraform?

**Resposta:** Para renomear ou mover recursos no código sem causar a destruição e recriação do recurso real.

---

## Flashcard 35
**Pergunta:** O que são `ephemeral values` na versão 004?

**Resposta:** Valores que existem apenas durante a execução do plano e não são persistidos no arquivo de estado.

---

## Flashcard 36
**Pergunta:** Qual funcionalidade do HCP Terraform permite organizar múltiplos workspaces?

**Resposta:** `Projects`

---

## Flashcard 37
**Pergunta:** Como o Terraform lida com segredos se eles forem passados como variáveis normais?

**Resposta:** Eles serão armazenados em texto claro no arquivo de estado.

---

## Flashcard 38
**Pergunta:** Qual ferramenta da HashiCorp é recomendada para gerenciar segredos e injetar credenciais no Terraform?

**Resposta:** HashiCorp Vault

---

## Flashcard 39
**Pergunta:** O que é o Sentinel no contexto do Terraform Enterprise/HCP?

**Resposta:** Um framework de política como código que impõe guardrails antes do `apply`.

---

## Flashcard 40
**Pergunta:** Qual é a diferença entre um backend local e um backend remoto?

**Resposta:** O local armazena o estado em disco; o remoto armazena em serviços como S3, Azure Blob ou HCP Terraform.

---

## Flashcard 41
**Pergunta:** O comando `terraform state list` tem qual função?

**Resposta:** Listar todos os recursos que estão atualmente registrados no arquivo de estado.

---

## Flashcard 42
**Pergunta:** O que o comando `terraform console` permite fazer?

**Resposta:** Testar e avaliar expressões da linguagem Terraform de forma interativa.

---

## Flashcard 43
**Pergunta:** Qual argumento é obrigatório em um bloco de `output`?

**Resposta:** `value`

---

## Flashcard 44
**Pergunta:** Se você omitir a restrição de versão ao referenciar um módulo no Registry, o que o Terraform fará?

**Resposta:** Usará automaticamente a versão mais recente disponível.

---

## Flashcard 45
**Pergunta:** Qual é a função do arquivo `.terraform` criado no diretório de trabalho?

**Resposta:** Funcionar como um cache para plugins de provedores e dados de módulos instalados.

---

## Flashcard 46
**Pergunta:** No HCP Terraform, o que são `Variable Sets`?

**Resposta:** Grupos de variáveis que podem ser aplicados a múltiplos workspaces simultaneamente.

---

## Flashcard 47
**Pergunta:** Qual recurso da versão 004 permite adicionar validações personalizadas a variáveis?

**Resposta:** Bloco de `validation` dentro da definição da variável.

---

## Flashcard 48
**Pergunta:** O que é `drift` no gerenciamento de estado?

**Resposta:** A divergência entre a configuração definida no código e o estado real da infraestrutura na nuvem.

---

## Flashcard 49
**Pergunta:** Qual comando é usado para autenticar a CLI do Terraform com o HCP Terraform?

**Resposta:** `terraform login`

---

## Flashcard 50
**Pergunta:** O que define um fluxo de trabalho `service-agnostic` no Terraform?

**Resposta:** A capacidade de usar a mesma linguagem (HCL) e fluxo (Plan/Apply) para qualquer provedor de serviço.

---

## Flashcard 51
**Pergunta:** Quantas operações concorrentes o Terraform realiza por padrão durante o `apply`?

**Resposta:** 10

---

## Flashcard 52
**Pergunta:** Qual é o impacto de uma dependência implícita?

**Resposta:** O Terraform analisa as referências entre recursos para determinar automaticamente a ordem de criação.

---

## Flashcard 53
**Pergunta:** O que o comando `terraform refresh` faz (antigo comportamento)?

**Resposta:** Reconcilia o arquivo de estado com as configurações reais sem alterar a infraestrutura.

---

## Flashcard 54
**Pergunta:** Como o Terraform identifica unicamente cada recurso em seu estado?

**Resposta:** Através do endereço do recurso (`tipo.nome_local`).

---

## Flashcard 55
**Pergunta:** Quais são os tipos de dados estruturados suportados pelo Terraform?

**Resposta:** `list`, `set`, `map`, `object` e `tuple`.

---

## Flashcard 56
**Pergunta:** O que o meta-argumento `for_each` faz em um bloco de recurso?

**Resposta:** Cria múltiplas instâncias de um recurso com base em uma coleção (mapa ou conjunto).

---

## Flashcard 57
**Pergunta:** Qual é a utilidade do bloco `dynamic`?

**Resposta:** Gerar blocos aninhados dentro de um recurso de forma repetitiva a partir de uma lista ou mapa.

---

## Flashcard 58
**Pergunta:** O comando `terraform state show <ENDEREÇO>` faz o quê?

**Resposta:** Exibe os atributos detalhados de um único recurso específico contido no estado.

---

## Flashcard 59
**Pergunta:** Qual recurso do HCP Terraform permite detectar `drift` automaticamente?

**Resposta:** Health / Drift Detection.

---

## Flashcard 60
**Pergunta:** O que acontece se o comando `terraform plan` falhar ao ler o estado?

**Resposta:** O plano é interrompido, pois o Terraform não consegue comparar a configuração com a realidade atual.

---

## Flashcard 61
**Pergunta:** Em relação à governança, o que o OPA (Open Policy Agent) permite no HCP Terraform?

**Resposta:** Aplicar políticas de segurança e conformidade baseadas na linguagem Rego.

---

## Flashcard 62
**Pergunta:** Qual a diferença entre o Terraform Community e o Terraform Enterprise?

**Resposta:** O Community é focado em execução local e CLI; o Enterprise oferece recursos avançados de colaboração, SSO e auditoria em infraestrutura própria.

---

## Flashcard 63
**Pergunta:** Como referenciar o valor de uma variável `instance_type` no código?

**Resposta:** `var.instance_type`
---

## Flashcard 64
**Pergunta:** O que define a ordem em que os recursos são destruídos pelo Terraform?

**Resposta:** O gráfico de dependências, sendo destruídos na ordem inversa da criação por padrão.

---

## Flashcard 65
**Pergunta:** Qual é o benefício de usar o Terraform Cloud/HCP como backend remoto em vez de um bucket S3 simples?

**Resposta:** Oferece interface UI, histórico de runs e integração nativa com VCS (Version Control Systems).

---

## Flashcard 66
**Pergunta:** O que significa 'Idempotency' (Idempotência) no Terraform?

**Resposta:** A propriedade de que executar o mesmo código várias vezes resultará no mesmo estado final, sem mudanças desnecessárias.

---

## Flashcard 67
**Pergunta:** Qual função HCL é usada para ler o conteúdo de um arquivo em uma string?

**Resposta:** file()

---

## Flashcard 68
**Pergunta:** Como converter um objeto em formato JSON usando HCL?

**Resposta:** jsonencode()

---

## Flashcard 69
**Pergunta:** O que o argumento `lifecycle { create_before_destroy = true }` faz?

**Resposta:**Garante que o novo recurso seja criado antes que o antigo seja destruído durante uma substituição.

---

## Flashcard 70
**Pergunta:** Qual comando é usado para migrar o estado de um backend local para o HCP Terraform?

**Resposta:**terraform init (após alterar o bloco terraform/cloud no código).

---

## Flashcard 71
**Pergunta:** Onde o Terraform armazena os plugins baixados no diretório de trabalho?

**Resposta:**No diretório oculto `.terraform/providers`.

---

## Flashcard 72
**Pergunta:** O que o comando `terraform graph` gera?

**Resposta:**Uma representação visual (em formato DOT) do gráfico de dependências dos recursos.

---

## Flashcard 73
**Pergunta:** Qual comando permite trocar de workspace no CLI?

**Resposta:**terraform workspace select

---

## Flashcard 74
**Pergunta:** Na versão 004, o que o bloco `removed` permite fazer?

**Resposta:**Declarar que um recurso foi removido da configuração para que o Terraform o esqueça no próximo apply sem destruí-lo.

---

## Flashcard 75
**Pergunta:** Como o Terraform trata múltiplos blocos `provider` com o mesmo nome?

**Resposta:**Exige o uso de um `alias` para diferenciá-los, permitindo múltiplas configurações (ex: diferentes regiões).

---

## Flashcard 76
**Pergunta:** Qual comando permite ver a versão atual instalada do Terraform CLI?

**Resposta:**terraform version

---

## Flashcard 77
**Pergunta:** O que é o 'Registry' do Terraform?

**Resposta:**Um repositório central para descobrir e compartilhar provedores e módulos.

---

## Flashcard 78
**Pergunta:** A saída do comando `terraform plan` pode ser salva em um arquivo?

**Resposta:**Sim, usando a flag `-out=<CAMINHO_DO_ARQUIVO>`.