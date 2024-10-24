# Mermaid-Copilot_TDCSummitIABrasilia
Materiais da apresentação "Inteligência Artificial + Documentação de Projetos -- Simplificando a geração de documentações com Inteligência Artificial". Palestra realizada durante o TDC Summit IA Brasília em 24/10/2024.

## Exemplos

### Fluxograma

Pergunta ao Copilot:

```
Gere para mim um diagrama em Mermaid que demonstre o fluxo de autenticação no GitHub, lembrando que se está utilizando MFA com OTP
```

Resposta:

```mermaid
flowchart TD
    A[Usuário] --> B[Entra com nome de usuário e senha]
    B --> C{O Login é válido?}
    C -- Sim --> D[GitHub solicita OTP]
    C -- Não --> H[Erro de autenticação]
    D --> E[Usuário abre o aplicativo autenticador]
    E --> F[Aplicativo autenticador gera OTP]
    F --> G[Usuário entra com OTP]
    G --> I{OTP válido?}
    I -- Sim --> J[Autenticação bem-sucedida]
    I -- Não --> H[Erro de autenticação]
```

---

### Diagrama de Sequência

Pergunta ao Copilot:

```
Gere para mim em Mermaid um diagrama de sequência que demonstre o fluxo para se autenticar em uma API protegida com o Azure API Management e que faz uso do Microsoft Entra ID...
```

Resposta:

```mermaid
sequenceDiagram
    participant ClientApp
    participant AzureAD as Microsoft Entra ID
    participant APIM as Azure API Management
    participant API

    ClientApp->>AzureAD: Solicita token de acesso
    AzureAD-->>ClientApp: Retorna token de acesso
    ClientApp->>APIM: Faz requisição à API com token de acesso
    APIM->>AzureAD: Valida token de acesso
    AzureAD-->>APIM: Token válido
    APIM->>API: Encaminha requisição à API
    API-->>APIM: Retorna resposta da API
    APIM-->>ClientApp: Retorna resposta da API
```