![Logotipo HelpApp](https://github.com/user-attachments/assets/4215d38c-c546-46b5-b446-9925d4d486f8)

📌 HelpApp
==========

Um aplicativo de gestão de atendimentos voluntários, desenvolvido com arquitetura limpa e princípios sólidos da engenharia de software.

📚 Descrição Geral
------------------

O **HelpApp** é um sistema para organizar atendimentos voluntários, focado em facilitar o encontro entre quem precisa de ajuda e quem pode ajudar. O projeto foi construído utilizando a plataforma **.NET Core**, com persistência em **SQL Server** e implantação na nuvem via **Azure Server Apps**. Toda a lógica foi projetada com base em princípios de desenvolvimento sustentável e manutenção facilitada, utilizando os conceitos do **SOLID**.

🧪 Funcionalidades
------------------

*   **Cadastro de usuários** (ajudante e solicitante).
    
*   **Registro e gerenciamento de atendimentos** (criação, edição e finalização).
    
*   **Agenda personalizada** para cada voluntário/ajudante.
    
*   **Histórico e relatórios de ações** realizadas.
    
*   **Login seguro** com autenticação e autorização.
    

🏗️ Arquitetura do Projeto
--------------------------

O projeto segue a **Clean Architecture**, separado em camadas e projetos distintos para manter as responsabilidades bem definidas e facilitar a manutenção e evolução:

*   **HelpApp.Domain**:
    
    *   Contém as entidades e regras de negócio.
        
    *   Define as interfaces de repositório (contratos) que a camada de infraestrutura deve implementar.
        
*   **HelpApp.Application**:
    
    *   Implementa os casos de uso (application services) e orquestra a lógica de negócio.
        
    *   Depende das interfaces definidas em Domain e não das implementações concretas.
        
*   **HelpApp.Infra.Data**:
    
    *   Responsável pela persistência de dados, implementando as interfaces do domínio.
        
    *   Contém os repositórios, configurações de banco de dados e mapeamentos.
        
*   **HelpApp.Infra.IoC**:
    
    *   Gerencia a configuração de Injeção de Dependência (IoC/DI).
        
    *   Define como as interfaces são vinculadas às implementações concretas.
        
*   **HelpApp.API**:
    
    *   Camada de apresentação (Interface).
        
    *   Exponde os endpoints (controllers) que interagem com a aplicação.
        
    *   Recebe as requisições HTTP e direciona para as classes de Application.
        
*   **HelpApp.DomainTest**:
    
    *   Projeto de testes que valida regras de negócio e comportamentos das entidades do domínio.
        
    *   Foca principalmente nas entidades e métodos do Domain.
        

⚙️ Princípios SOLID Aplicados
-----------------------------

### 5.1. S - Single Responsibility Principle

Cada classe tem uma única responsabilidade.  
**Exemplo**: A classe `UserManager` trata apenas da lógica de criação e atualização de usuários, sem interferir em regras de agendamento ou autenticação.

### 5.2. O - Open/Closed Principle

O sistema está aberto para extensão, mas fechado para modificação.  
**Exemplo**: Interfaces como `IUserRepository` e `IAttendanceService` permitem novas implementações sem alterar o código existente.

### 5.3. L - Liskov Substitution Principle

Subclasses devem poder substituir superclasses sem alterar o comportamento do sistema.  
**Exemplo**: Serviços de notificação como `EmailNotifier` e `SmsNotifier` herdam de uma interface comum e podem ser trocados sem quebrar funcionalidades.

### 5.4. I - Interface Segregation Principle

Interfaces específicas são melhores que interfaces genéricas que obrigam a implementação de métodos desnecessários.  
**Exemplo**: O HelpApp usa interfaces distintas para contextos diferentes, como `ILoginService` e `IAgendaManager`, evitando que uma classe precise implementar métodos que não utiliza.

### 5.5. D - Dependency Inversion Principle

Os módulos de alto nível não devem depender dos de baixo nível; ambos devem depender de abstrações.  
**Exemplo**: A camada de aplicação depende de interfaces (definidas em Domain) e não diretamente de implementações concretas ou do SQL Server. Isso torna o código desacoplado e testável.

🧩 Tecnologias e Ferramentas
----------------------------

*   **Linguagem:** C# (.NET Core)
    
*   **Banco de Dados:** SQL Server
    
*   **Ambiente:** Azure App Services
    
*   **IDE:** Visual Studio / VS Code
    
*   **ORM:** Entity Framework Core
    
*   **Testes:** xUnit ou NUnit
    
*   **Controle de Versão:** Git + GitHub
    

🔧 Como Rodar o Projeto
-----------------------

1.  **Clonar o repositório**:
    
    `git clone https://github.com/usuario/helpapp-backend.git` 
    
2.  **Abrir no Visual Studio** (ou VS Code).
    
3.  **Configurar a string de conexão** no `appsettings.json` (localizado em `HelpApp.API` ou em `HelpApp.Infra.Data`, conforme a sua configuração).
    
4.  **Aplicar as migrations**:
    
    `cd HelpApp.Infra.Data
    dotnet ef database update` 
    
    Ou via Package Manager Console (Visual Studio):
    
    `Update-Database` 
    
5.  **Executar a aplicação**:
    
    *   No Visual Studio: pressione `F5`.
        
    *   Via CLI:
        
        `cd HelpApp.API
        dotnet run` 
        
6.  **Testar rotas**:
    
    *   Pode-se usar **Swagger** (se configurado) acessando `https://localhost:<porta>/swagger`.
        
    *   Ou usar ferramentas como **Postman** para enviar requisições.
        

🧪 Testes Automatizados
-----------------------

*   **Camadas com testes**: principalmente o **Domain**, no projeto **HelpApp.DomainTest**, validando regras de negócio e entidades.
    
*   **Para rodar os testes**:
    
    `dotnet test` 
    
*   **Ferramentas**: xUnit ou NUnit (dependendo de qual foi configurado).
    
*   **Cobertura priorizada**: regras de negócio e serviços críticos.
    

📂 **Estrutura de Pastas**
--------------------------

Abaixo, um diagrama consolidado, mostrando a relação entre as pastas/projetos e as subestruturas comuns (como Entities, Interfaces, UseCases, etc.):

```
HelpApp/
├── HelpApp.API/               # Responsável pela comunicação com o cliente, expondo os endpoints da API
│   ├── Controllers/           # Controladores que gerenciam as requisições da API
│   └── Properties/            # Arquivos de configuração específicos da API, como settings
│
├── HelpApp.Application/       # Contém a lógica da aplicação, incluindo casos de uso e serviços
│   └── Services/              # Serviços de apoio que implementam a lógica de negócios
│
├── HelpApp.Domain/            # Camada onde reside a lógica de negócio e abstrações de persistência
│   ├── Entities/              # Definição das entidades principais do sistema (usuário, produtos, etc.)
│   ├── Interfaces/            # Interfaces para abstração de repositórios e outros serviços
│   └── Validation/            # Validações relacionadas a regras de negócio específicas das entidades
│
├── HelpApp.Domain.Test/       # Testes unitários que validam as regras e comportamentos da camada de domínio
│
├── HelpApp.Infra.Data/        # Camada de infraestrutura para persistência e integração com recursos externos
│   └── Repositories/          # Implementações dos repositórios que interagem com o banco de dados
│
└── HelpApp.Infra.IoC/         # Configuração da injeção de dependências para toda a aplicação

```

*   **HelpApp.API**: Responsável pela camada de apresentação (Controllers, Endpoints, DTOs, Program.cs).
    
*   **HelpApp.Application**: Lógica de negócio e casos de uso (Application Services, UseCases).
    
*   **HelpApp.Domain**: Entidades e interfaces (regras de negócio e contratos de repositório).
    
*   **HelpApp.DomainTest**: Testes de unidade para validar o comportamento do domínio.
    
*   **HelpApp.Infra.Data**: Persistência de dados (repositórios, configurações de banco e migrations).
    
*   **HelpApp.Infra.IoC**: Configurações de Injeção de Dependência para manter o código desacoplado.

    

👨‍💻 Autores
-------------

*   Ramon dos Santos - Frontend, Backend, Testes e Documentação - [GitHub](https://github.com/RamonSantos10)
    

📜 Licença
----------

Este projeto está sob a licença **MIT**.
