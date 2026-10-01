# Laboratório Prático: Arquitetura de Identidade Zero Trust no Microsoft Entra ID

## Objetivo do Projeto
Este projeto tem como objetivo implementar uma arquitetura de segurança em nuvem baseada no princípio de Zero Trust (Confiança Zero). A infraestrutura foi configurada no Microsoft Entra ID (antigo Azure AD) para garantir que o acesso aos recursos do Azure siga estritamente o princípio do menor privilégio e exija verificação explícita contínua. O laboratório consolida na prática os fundamentos de gestão de identidade e acesso (IAM), operando controles avançados de proteção contra credenciais comprometidas e movimentação lateral.

## Tecnologias e Recursos Utilizados
* **Plataforma:** Microsoft Azure & Microsoft Entra ID (Tenant Corporativo / Premium P2)
* **RBAC:** Role-Based Access Control (Controle de Acesso Baseado em Função)
* **Conditional Access:** Políticas de Acesso Condicional com exigência de MFA
* **Azure PIM:** Privileged Identity Management (Acesso Just-In-Time)
* **Monitoramento:** Entra ID Sign-in Logs e ferramentas de auditoria

## Cenário e Arquitetura Implementada
A simulação consistiu na criação de um ambiente corporativo com separação de funções operacionais, aplicando camadas progressivas de proteção:

### 1. Governança de Identidade e Agrupamento Lógico
Criação de identidades nativas na nuvem para simular diferentes perfis operacionais (`Administrador Cloud` e `Auditor de Segurança`). A governança foi estruturada em Grupos de Segurança, garantindo que o provisionamento de permissões seja feito em massa e de forma escalável.
  <img width="1596" height="618" alt="Users_EntraID" src="https://github.com/user-attachments/assets/2521fabf-3d0c-475d-a588-e2fea78b8c8b" />

### 2. Controle de Acesso Baseado em Função (RBAC)
Provisionamento de um *Resource Group* (`RG-Laboratorio-Sec`) atuando como o contêiner dos ativos de infraestrutura. O princípio do menor privilégio foi aplicado na camada de recursos: o grupo de administração recebeu a função de **Contributor**, enquanto o grupo de auditoria recebeu a restrita função de **Reader**.
  <img width="1885" height="837" alt="IAM" src="https://github.com/user-attachments/assets/b3fae97b-15b3-4fb7-beed-bdfcfea9604e" />

### 3. Controles Dinâmicos e Acesso Condicional (Zero Trust)
Implementação de políticas de *Conditional Access* atuando como o perímetro de segurança moderno. A regra configurada bloqueia o acesso por padrão caso a tentativa de login não satisfaça a exigência de Autenticação Multifator (MFA), mitigando o risco de credenciais vazadas.
  <img width="1780" height="677" alt="AcessoCondicional" src="https://github.com/user-attachments/assets/fae95a7c-90b6-4873-bb5c-08ef77c704b4" />

### 4. Elevação de Privilégio Just-In-Time (PIM)
Eliminação do vetor de risco de contas superprivilegiadas permanentes. A função administrativa de *Global Reader* foi integrada ao Azure PIM. O acesso privilegiado passou a exigir ativação sob demanda (Just-In-Time), com aprovação e prazo de expiração predefinido.
  <img width="1867" height="515" alt="PIM" src="https://github.com/user-attachments/assets/42820a70-6ea4-47cc-b281-332839caf3e7" />

### 5. Rastreabilidade e Operações de Segurança
Validação contínua através da análise de *Sign-in logs* (Logs de entrada). O rastreamento detalhado do comportamento de autenticação permitiu validar a eficácia da política de Acesso Condicional durante as tentativas de login.

## Conclusão
A implementação bem-sucedida desta infraestrutura demonstra a capacidade de traduzir requisitos teóricos de Defesa Cibernética em configurações técnicas sólidas dentro de um ecossistema real de nuvem. A orquestração simultânea de RBAC, Conditional Access e PIM substitui o antigo conceito de "rede confiável" por um perímetro focado em identidade, garantindo que o acesso correto seja concedido apenas à identidade correta, no momento certo.
