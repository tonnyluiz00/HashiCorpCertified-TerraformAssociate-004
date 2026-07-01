# Quiz 01

## Pergunta 1
**Ao utilizar o comando `terraform state rm` em um recurso específico, qual é o impacto imediato na infraestrutura real gerenciada por esse recurso?**

- A. O recurso é destruído permanentemente na infraestrutura do provedor de nuvem.
- B. O Terraform marca o recurso como "depreciado" no arquivo de configuração `.tf`.
- C. O recurso entra em um ciclo de reinicialização para sincronizar com o novo estado.
- D. O recurso continua existindo na nuvem, mas o Terraform deixa de gerenciá-lo.

**Resposta:** D

**Motivo:** O comando desvincula o objeto do estado do Terraform, fazendo com que o Terraform "esqueça" sua existência enquanto ele permanece ativo no provedor.

---

## Pergunta 2
**No Terraform Associate 004, qual é a principal função do bloco de ciclo de vida (`lifecycle`) com o argumento `create_before_destroy = true`?**

- A. Permite que o Terraform ignore erros de API durante a fase de destruição de recursos críticos.
- B. Força a recriação do recurso em cada execução do `terraform apply`, independentemente de mudanças.
- C. Garante que o Terraform valide o plano de execução antes de destruir qualquer recurso órfão.
- D. Altera o comportamento padrão para criar um novo recurso substituto antes de remover o recurso antigo.

**Resposta:** D

**Motivo:** Esse argumento é essencial para evitar tempo de inatividade, garantindo que a nova instância esteja operacional antes da exclusão da anterior.

---

## Pergunta 3
**Qual é uma limitação fundamental do comando `terraform import` ao trazer infraestrutura existente para o gerenciamento do Terraform?**

- A. O comando não gera automaticamente os blocos de configuração HCL correspondentes no seu código.
- B. Ele só pode importar recursos que foram criados originalmente através do Console da AWS ou Azure.
- C. A importação exige que o arquivo de estado esteja obrigatoriamente armazenado em um backend local.
- D. Ele apaga todas as tags e metadados do recurso original durante o processo de mapeamento.

**Resposta:** A

**Motivo:** O import mapeia o recurso para o estado, mas exige que o usuário escreva manualmente o bloco de recurso no arquivo `.tf` para coincidir com o estado.

---

## Pergunta 4
**Ao utilizar o modo refresh-only (`terraform apply -refresh-only`), o que exatamente o Terraform está autorizado a modificar?**

- A. Apenas os arquivos de configuração `.tf` para refletir mudanças externas.
- B. Exclusivamente o arquivo de estado (`state file`) para alinhar-se com a realidade da nuvem.
- C. Os recursos na nuvem que apresentam divergências em relação ao código.
- D. As permissões de acesso do provedor de nuvem para garantir a segurança do estado.

**Resposta:** B

**Motivo:** Esse modo é usado para detectar drift e atualizar o estado sem propor alterações de criação, modificação ou destruição de recursos reais.

---

## Pergunta 5
**Como a funcionalidade de `Custom Validation` (introduzida recentemente e cobrada na versão 004) auxilia no gerenciamento de módulos?**

- A. Permite definir regras gramaticais personalizadas que substituem o padrão HCL do Terraform.
- B. Permite que autores de módulos definam condições e mensagens de erro específicas para variáveis de entrada.
- C. Ela verifica automaticamente se o provedor de nuvem possui cotas suficientes antes de iniciar o plano.
- D. Garante que o módulo seja compatível com todas as versões anteriores do Terraform.

**Resposta:** B

**Motivo:** Blocos de validação garantem que usuários do módulo forneçam entradas que façam sentido lógico, evitando falhas tardias no `apply`.
