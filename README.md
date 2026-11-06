
# Introdução

Este trabalho apresenta a realização de testes de caixa cinza em uma API de autenticação, utilizando o Supabase e o Postman.

O Supabase foi utilizado para configurar a autenticação de usuários, enquanto o Postman permitiu enviar requisições HTTP e analisar as respostas retornadas pela API.

# Objetivo da Atividade

O objetivo foi verificar o comportamento de uma API de autenticação em diferentes situações, incluindo login correto, senha incorreta, usuário inexistente, campos vazios e credenciais inválidas.

Os testes foram realizados com conhecimento parcial do funcionamento da API, como endpoint, cabeçalhos e estrutura do corpo das requisições.

# Configuração do Supabase

Foi criado um projeto chamado `trabalho-caixa-cinza` na plataforma Supabase.

Após a criação, foi verificado que a autenticação por e-mail estava habilitada. Também foi cadastrado um usuário de teste para realizar as requisições de login.

Foram identificadas a URL do projeto e a chave pública da API, utilizadas posteriormente na configuração do Postman.

**Evidências:**

- [Projeto Supabase](prints/07-projeto-supabase.png)
- [Autenticação por e-mail](prints/08-autenticacao-email.png)
- [Usuário cadastrado](prints/09-usuario-criado.png)
- [Chave pública da API](prints/10-credenciais-api.png)

# Configuração do Postman

Foi criado um Workspace chamado `Testes Caixa Cinza - Supabase` e uma coleção chamada `Testes de Autenticação - Supabase`.

Também foi configurado um Environment chamado `Supabase - Testes`, contendo quatro variáveis:

- `base_url`: URL do projeto Supabase.
- `api_key`: chave pública da API.
- `email`: e-mail do usuário cadastrado.
- `password`: senha do usuário de teste.

Os valores das variáveis foram deixados em branco no arquivo de Environment exportado, evitando a publicação de credenciais privadas.

**Evidências:**

- [Workspace e coleção](prints/11-workspace-postman.png)
- [Environment](prints/12-environment-postman.png)

**Arquivos exportados do Postman:**

- [Coleção de testes](postman/testes-autenticacao-supabase.postman_collection.json)
- [Environment](postman/supabase-testes.postman_environment.json)

# Configuração das Requisições

As requisições utilizaram o método HTTP `POST` e o seguinte endpoint:

```http
POST {{base_url}}/auth/v1/token?grant_type=password
```

Foram configurados os seguintes cabeçalhos:

| Header | Valor |
|---|---|
| apikey | `{{api_key}}` |
| Authorization | `Bearer {{api_key}}` |
| Content-Type | `application/json` |

Exemplo do corpo JSON utilizado no login válido:

```json
{
  "email": "{{email}}",
  "password": "{{password}}"
}
```

Para os demais testes, os valores de e-mail e senha foram alterados conforme o cenário.

**Evidência:**

- [Headers da requisição](prints/13-headers-postman.png)

# Execução dos Testes

Foram executados cinco testes de autenticação pelo Postman.

| ID | Cenário | Resultado esperado | Resultado obtido | Status |
|---|---|---|---|---|
| 01 | Login válido | HTTP 200 e token de acesso | HTTP 200, com `access_token` retornado | Sucesso |
| 02 | Senha incorreta | Erro de autenticação | HTTP 400 - `invalid_credentials` | Sucesso |
| 03 | Usuário inexistente | Acesso negado | HTTP 400 - `invalid_credentials` | Sucesso |
| 04 | Campos vazios | Erro de validação | HTTP 400 - `validation_failed` | Sucesso |
| 05 | Credenciais inválidas | Erro de autenticação | HTTP 400 - `invalid_credentials` | Sucesso |

Todos os cenários apresentaram os comportamentos esperados.

O código HTTP 400 nos testes negativos não representa uma falha da atividade, pois o objetivo desses cenários era verificar se a API rejeitava entradas inválidas.

**Evidências dos testes:**

- [Teste 01 - Login válido](prints/01%20-%20Senha%20Correta.png)
- [Teste 02 - Senha incorreta](prints/02%20-%20Senha%20Incorrteta.png)
- [Teste 03 - Usuário inexistente](prints/03%20-%20Usu%C3%A1rio%20Inexistente.png)
- [Teste 04 - Campos vazios](prints/04%20-%20Campos%20Vazios.png)
- [Teste 05 - Credenciais inválidas](prints/05-credenciais-invalidas.png)

# Registro dos Testes

Os resultados foram registrados em uma planilha Excel, contendo os seguintes campos:

- ID do teste
- Cenário
- Entrada
- Resultado esperado
- Resultado obtido
- Status
- Observações

A planilha foi utilizada para organizar os resultados e facilitar a comparação entre o comportamento esperado e o observado.

**Arquivos:**

- [Planilha de testes](planilha/planilha_testes_caixa_cinza.xlsx)
- [Print da planilha](prints/06-planilha-testes.png)

# Resultados Obtidos

No teste de login válido, a API retornou o código HTTP 200 e um token de acesso, confirmando que a autenticação foi realizada.

Nos testes com senha incorreta, usuário inexistente e credenciais inválidas, a API retornou HTTP 400 com o código `invalid_credentials` e a mensagem `Invalid login credentials`.

No teste com os campos vazios, a resposta foi HTTP 400 com o código `validation_failed` e a mensagem `missing email or phone`, indicando ausência de informações necessárias para a autenticação.

Os cinco testes tiveram resultados compatíveis com o esperado.

**Resumo dos resultados:**

| Indicador | Resultado |
|---|---|
| Total de cenários executados | 5 |
| Cenários com comportamento esperado | 5 |
| Cenários com comportamento inesperado | 0 |
| Taxa de conformidade dos cenários | 100% |

Não foram identificadas falhas funcionais nos cenários executados. Esse resultado se limita aos cinco testes realizados e não representa uma validação completa de toda a API.

# Conclusão

A atividade permitiu compreender melhor o funcionamento de uma API de autenticação e a importância dos testes de caixa cinza.

Durante a execução, foi possível praticar a configuração do Supabase, o uso de variáveis no Postman, o envio de requisições HTTP e a interpretação das respostas em JSON.

Uma dificuldade encontrada foi configurar corretamente as variáveis do Environment para que o Postman reconhecesse a URL da API.

Como melhoria, seria interessante automatizar a execução dos testes no Postman, facilitando novas verificações após alterações no sistema.

Os resultados mostraram que a API respondeu adequadamente aos cinco cenários testados, demonstrando a importância dos testes funcionais para verificar a autenticação de usuários.
