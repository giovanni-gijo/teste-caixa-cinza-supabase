\# Introdução



Este trabalho apresenta a realização de testes de caixa cinza em uma API de autenticação, utilizando o Supabase e o Postman.



O Supabase foi utilizado para configurar a autenticação de usuários, enquanto o Postman permitiu enviar requisições HTTP e analisar as respostas retornadas pela API.



\# Objetivo da Atividade



O objetivo foi verificar o comportamento de uma API de autenticação em diferentes situações, incluindo login correto, senha incorreta, usuário inexistente, campos vazios e credenciais inválidas.



Os testes foram realizados com conhecimento parcial do funcionamento da API, como endpoint, cabeçalhos e estrutura do corpo das requisições.



\# Configuração do Supabase



Foi criado um projeto chamado `trabalho-caixa-cinza` na plataforma Supabase.



Após a criação, foi verificado que a autenticação por e-mail estava habilitada. Também foi cadastrado um usuário de teste para realizar as requisições de login.



Foram identificadas a URL do projeto e a chave pública da API, utilizadas posteriormente na configuração do Postman.



\*\*Evidências:\*\*



\- \[Projeto Supabase](prints/07-projeto-supabase.png)

\- \[Autenticação por e-mail](prints/08-autenticacao-email.png)

\- \[Usuário cadastrado](prints/09-usuario-criado.png)

\- \[Chave pública da API](prints/10-credenciais-api.png)



\# Configuração do Postman



Foi criado um Workspace chamado `Testes Caixa Cinza - Supabase` e uma coleção chamada `Testes de Autenticação - Supabase`.



Também foi configurado um Environment chamado `Supabase - Testes`, contendo quatro variáveis:



\- `base\_url`: URL do projeto Supabase.

\- `api\_key`: chave pública da API.

\- `email`: e-mail do usuário cadastrado.

\- `password`: senha do usuário de teste.



Os valores privados não foram incluídos nos arquivos exportados.



\*\*Evidências:\*\*



\- \[Workspace e coleção](prints/11-workspace-postman.png)

\- \[Environment](prints/12-environment-postman.png)



\# Configuração das Requisições



As requisições utilizaram o método HTTP `POST` e o seguinte endpoint:



`{{base\_url}}/auth/v1/token?grant\_type=password`



Foram configurados os seguintes cabeçalhos:



| Header | Valor |

|---|---|

| apikey | `{{api\_key}}` |

| Authorization | `Bearer {{api\_key}}` |

| Content-Type | `application/json` |



Exemplo do corpo JSON utilizado no login válido:



```json

{

&#x20; "email": "{{email}}",

&#x20; "password": "{{password}}"

}

```



Para os demais testes, os valores de e-mail e senha foram alterados conforme o cenário.



\*\*Evidência:\*\*



\- \[Headers da requisição](prints/13-headers-postman.png)



\# Execução dos Testes



Foram executados cinco testes de autenticação pelo Postman.



| ID | Cenário | Resultado esperado | Resultado obtido |

|---|---|---|---|

| 01 | Login válido | HTTP 200 e token de acesso | HTTP 200, com token retornado |

| 02 | Senha incorreta | Erro de autenticação | HTTP 400 - invalid\_credentials |

| 03 | Usuário inexistente | Acesso negado | HTTP 400 - invalid\_credentials |

| 04 | Campos vazios | Erro de validação | HTTP 400 - validation\_failed |

| 05 | Credenciais inválidas | Erro de autenticação | HTTP 400 - invalid\_credentials |



Todos os cenários apresentaram os comportamentos esperados.



\# Registro dos Testes



Os resultados foram registrados em uma planilha Excel, contendo identificação do teste, cenário, entrada, resultado esperado, resultado obtido, status e observações.



A planilha foi utilizada para organizar os resultados e facilitar a comparação entre o comportamento esperado e o observado.



\*\*Arquivos:\*\*



\- \[Planilha de testes](planilha/planilha\_testes\_caixa\_cinza.xlsx)

\- \[Print da planilha](prints/06-planilha-testes.png)



\# Resultados Obtidos



No teste de login válido, a API retornou o código HTTP 200 e um token de acesso, confirmando que a autenticação foi realizada.



Nos testes com senha incorreta, usuário inexistente e credenciais inválidas, a API retornou HTTP 400 com o código `invalid\_credentials`.



No teste com os campos vazios, a resposta foi HTTP 400 com o código `validation\_failed`, indicando ausência de informações necessárias para a autenticação.



Os cinco testes tiveram resultados compatíveis com o esperado. Não foram identificadas falhas funcionais nos cenários executados.



\*\*Evidências dos testes:\*\*



As capturas das cinco requisições estão disponíveis na pasta `prints`, com os respectivos códigos HTTP e respostas JSON.



\# Conclusão



A atividade permitiu compreender melhor o funcionamento de uma API de autenticação e a importância dos testes de caixa cinza.



Durante a execução, foi possível praticar a configuração do Supabase, o uso de variáveis no Postman, o envio de requisições HTTP e a interpretação das respostas em JSON.



Uma dificuldade encontrada foi configurar corretamente as variáveis do Environment para que o Postman reconhecesse a URL da API.



Como melhoria, seria interessante automatizar a execução dos testes no Postman, facilitando novas verificações após alterações no sistema.



Os resultados mostraram que a API respondeu adequadamente aos cinco cenários testados.

