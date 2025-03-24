# Mermaid-Copilot_TDCSummitIABrasilia
Materiais da apresentação "Inteligência Artificial + Documentação de Projetos -- Utilizando GitHub Copilot + Mermaid para documentar soluções". Palestra realizada durante o TDC Summit IA Brasília em 24/10/2024.

---

31 pessoas

24/10/2024 (quinta-feira)

---

---

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

### Diagrama de classes

Gerando um diagrama de classes para a implementação:

```csharp
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;
using System.Text.Json.Serialization;

namespace BenchmarkingDapperEFCoreCRMPostgres.EFCore;

public class Empresa
{
    [Key]
    public int IdEmpresa { get; set; }
    public string? CNPJ { get; set; }
    public string? Nome { get; set; }
    public string? Cidade { get; set; }
    public List<Contato>? Contatos { get; set; }
}

public class Contato
{
    [Key]
    public int IdContato { get; set; }
    public string? Nome { get; set; }
    public string? Telefone { get; set; }

    [ForeignKey("IdEmpresa")]
    [JsonIgnore]
    public Empresa? EmpresaRepresentada { get; set; }
}
```

Resposta do Copilot:

```mermaid
classDiagram
    class Empresa {
        int IdEmpresa
        string? CNPJ
        string? Nome
        string? Cidade
        List~Contato~? Contatos
    }

    class Contato {
        int IdContato
        string? Nome
        string? Telefone
        Empresa? EmpresaRepresentada
    }

    Empresa "1" --> "0..*" Contato : Contatos
    Contato --> Empresa : EmpresaRepresentada
```

---

### Diagrama de Estados

Pergunta ao Copilot:

```
Gere para mim em Mermaid um diagrama de estados representando um fluxo de aprovação de pull requests no GitHub e execução automatizada de workflows quando isso acontecer...
```

Resposta:

```mermaid
stateDiagram-v2
    [*] --> Aberto
    Aberto --> Revisão: Pull request criado
    Revisão --> Aprovado: Pull request aprovado
    Revisão --> Rejeitado: Pull request rejeitado
    Aprovado --> Merge: Pull request mesclado
    Merge --> Workflow: Workflow automatizado iniciado
    Workflow --> Concluído: Workflow concluído
    Rejeitado --> Fechado: Pull request fechado
    Concluído --> [*]
    Fechado --> [*]
```

---

### Diagrama de Entidades-Relacionamentos

Pergunta ao Copilot:

```
Gere para mim em Mermaid um diagrama de entidades-relacionamentos para o seguinte script:
```

```sql
CREATE DATABASE BaseCRMEF;

USE BaseCRMEF;

CREATE TABLE Empresas (
    IdEmpresa INT AUTO_INCREMENT NOT NULL,
    CNPJ CHAR(14) NOT NULL,
    Nome VARCHAR(100) NOT NULL,
    Cidade VARCHAR(50) NOT NULL,
    PRIMARY KEY (IdEmpresa)
);

CREATE TABLE Contatos (
    IdContato INT AUTO_INCREMENT NOT NULL,
    Nome VARCHAR(100) NOT NULL,
    Telefone VARCHAR(20) NOT NULL,
    IdEmpresa INT NOT NULL,
    PRIMARY KEY (IdContato),
    FOREIGN KEY (IdEmpresa) REFERENCES Empresas(IdEmpresa)
);
```

Resposta:

```mermaid
erDiagram
    EMPRESAS {
        INT IdEmpresa PK "AUTO_INCREMENT NOT NULL"
        CHAR CNPJ "14 NOT NULL"
        VARCHAR Nome "100 NOT NULL"
        VARCHAR Cidade "50 NOT NULL"
    }

    CONTATOS {
        INT IdContato PK "AUTO_INCREMENT NOT NULL"
        VARCHAR Nome "100 NOT NULL"
        VARCHAR Telefone "20 NOT NULL"
        INT IdEmpresa FK "NOT NULL"
    }

    EMPRESAS ||--o{ CONTATOS : "IdEmpresa"
```

---

### Mindmap

Pergunte ao Copilot:

```
Gere para mim um mindmap em Mermaid com tópicos, conceitos e ferramentas importantes para se trabalhar ou adotar a cultura DevOps
```

Resposta:

```mermaid
mindmap
  root((DevOps))
    subtopic1(Integração Contínua)
      subtopic1a(Jenkins)
      subtopic1b(Travis CI)
      subtopic1c(GitHub Actions)
      subtopic1d(Azure Pipelines)
    subtopic2(Entrega Contínua)
      subtopic2a(Spinnaker)
      subtopic2b(Argo CD)
      subtopic2c(GitLab CI/CD)
      subtopic2d(Azure Pipelines)
    subtopic3(Infrastructure as Code)
      subtopic3a(Terraform)
      subtopic3b(Ansible)
      subtopic3c(Puppet)
      subtopic3d(Chef)
      subtopic3e(Azure Resource Manager)
    subtopic4(Monitoramento e Log)
      subtopic4a(Prometheus)
      subtopic4b(Grafana)
      subtopic4c(ELK Stack)
      subtopic4d(Azure Monitor)
    subtopic5(Containerização)
      subtopic5a(Docker)
      subtopic5b(Kubernetes)
      subtopic5c(OpenShift)
      subtopic5d(Azure Kubernetes Service)
      subtopic5e(KEDA)
    subtopic6(Colaboração e Comunicação)
      subtopic6a(Slack)
      subtopic6b(Microsoft Teams)
      subtopic6c(Jira)
      subtopic6d(Azure Boards)
    subtopic7(Controle de Versão)
      subtopic7a(Git)
      subtopic7b(GitHub)
      subtopic7c(GitLab)
      subtopic7d(Azure Repos)
```
