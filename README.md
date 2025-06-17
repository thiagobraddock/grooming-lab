# 🤖 GPT Grooming Lab

Este repositório foi criado para demonstrar o uso de **GPTs personalizados integrados ao GitHub**, com foco no **refinamento de issues técnicas** utilizando inteligência artificial.

## 💡 Objetivo

Prototipar e demonstrar um agente de IA que ajude times ágeis a:

- Avaliar e refinar automaticamente issues mal descritas
- Sugerir estrutura padrão com INVEST, critérios Gherkin, subtarefas e dependências
- Padronizar a documentação e acelerar o processo de grooming

## 🚀 Como funciona

1. O usuário informa:
   - Usuário do GitHub (`owner`)
   - Nome do repositório (`repo`)
   - Número da issue (`issue_number`)
2. A GPT Action consulta a API do GitHub para buscar os detalhes da issue
3. O GPT analisa o conteúdo e retorna um refinamento automático, com sugestões padronizadas

---

## 🔧 Exemplo de uso da Action

GET https://api.github.com/repos/thiagobraddock/grooming-lab/issues/1  

Exemplo de preenchimento no GPT:

- **Owner:** `thiagobraddock`
- **Repo:** `grooming-lab`
- **Issue Number:** `1`

---

## 📄 Esquema da API (OpenAPI)

```yaml
openapi: 3.1.0
info:
  title: GitHub Issue Getter
  version: 1.0.0
servers:
  - url: https://api.github.com
paths:
  /repos/{owner}/{repo}/issues/{issue_number}:
    get:
      operationId: getGithubIssue
      summary: Buscar detalhes de uma issue no GitHub
      parameters:
        - name: owner
          in: path
          required: true
          schema:
            type: string
        - name: repo
          in: path
          required: true
          schema:
            type: string
        - name: issue_number
          in: path
          required: true
          schema:
            type: integer
      responses:
        "200":
          description: Sucesso na resposta da issue
          content:
            application/json:
              schema:
                type: object
                properties:
                  title:
                    type: string
                  body:
                    type: string
                  labels:
                    type: array
                    items:
                      type: object
                      properties:
                        name:
                          type: string
                  assignees:
                    type: array
                    items:
                      type: object
                      properties:
                        login:
                          type: string

  ```
