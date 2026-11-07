# Teste de Caixa Cinza — Supabase Auth e Postman

**Aluno:** Guilherme Cintra Doraciotto — RA 200376  
**Instituição:** FACENS — Análise e Desenvolvimento de Sistemas  
**Disciplina:** Teste de Software  
**Atividade:** Teste individual de caixa cinza com Supabase e Postman  
**Data da execução:** 07/11/2026  
**Situação:** 5 testes executados no Postman Desktop; 15/15 asserções aprovadas. As cinco evidências dos cenários e três capturas de configuração do Supabase estão publicadas; demais evidências de configuração ainda pendentes.

## Introdução

Teste de caixa cinza combina a observação do comportamento externo da aplicação com conhecimento parcial de sua estrutura. Nesta atividade, foi testada a API REST de autenticação por e-mail e senha do Supabase, utilizando o Postman para enviar requisições HTTP e verificar respostas, códigos de status e campos JSON.

## Objetivo da Atividade

Validar cinco situações de autenticação por senha: login válido, senha incorreta, usuário inexistente, campos vazios e credenciais inválidas. As avaliações verificam se o serviço retorna um token apenas para credenciais válidas e rejeita corretamente entradas inválidas.

## Configuração do Supabase

- **Projeto:** Teste-Caixa-Cinza-Postman
- **Região:** sa-east-1 (São Paulo)
- **Status durante a configuração:** ACTIVE_HEALTHY
- **Endpoint base:** https://alvxxaauygdtlgbtqyty.supabase.co
- **Autenticação:** e-mail e senha
- **Usuário de teste:** 1 usuário cadastrado com e-mail confirmado; dados pessoais e senha omitidos deste repositório.
- Não foi necessário criar tabelas de banco de dados para os testes.

**Segurança:** o repositório não contém a senha real do usuário, refresh tokens, access tokens ou chaves de administração do Supabase.

## Configuração do Postman

Criado Workspace pessoal **Teste Caixa Cinza - Supabase** e coleção **Teste Caixa Cinza - Supabase Auth (5 cenários)**, contendo cinco requisições POST.

O Environment **Supabase - Caixa Cinza - Testes** define `base_url`, `api_key` (chave publicável de baixo privilégio), `email`, `password` e variáveis de entradas inválidas. O exemplo disponibilizado neste repositório deixa valores sensíveis vazios. O valor de `password` foi informado localmente pelo aluno no Postman Desktop, sem publicá-lo.

**Importação:** importar os dois JSON da pasta `postman/`, selecionar o Environment e preencher localmente as variáveis em branco. Se já estiverem sincronizados na conta, não é preciso importar novamente.

## Configuração das Requisições

**Método:** `POST`  
**URL:** `{{base_url}}/auth/v1/token?grant_type=password`  
**Headers:** `apikey: {{api_key}}`, `Content-Type: application/json`.  
**Body (JSON):** campos `email` e `password` com valores distintos conforme cada cenário.

Com uma chave moderna `sb_publishable_...`, **não** enviar essa chave como `Authorization: Bearer`; o modelo deixa o header Authorization desabilitado. Nunca usar `service_role` nem `sb_secret_...` nos testes.

## Execução dos Testes

Os cinco cenários abaixo foram **executados pelo aluno no Postman Desktop** em 07/11/2026. Os resultados foram documentados a partir das capturas da ferramenta, que mostraram as respostas e a aba de testes.

| ID | Cenário | Entrada | HTTP esperado | HTTP observado | Asserções | Resultado |
|---|---|---|---:|---:|---:|---|
| TC01 | Login válido | Usuário cadastrado + senha correta | 200 | **200** | **3/3** | Aprovado |
| TC02 | Senha incorreta | Mesmo usuário + senha incorreta | 4xx | **400** | **3/3** | Aprovado |
| TC03 | Usuário inexistente | E-mail inexistente + senha fictícia | 4xx | **400** | **3/3** | Aprovado |
| TC04 | Campos vazios | E-mail e senha vazios | 4xx | **400** | **3/3** | Aprovado |
| TC05 | Credenciais inválidas | E-mail malformado + senha inválida | 4xx | **400** | **3/3** | Aprovado |

**Resultado consolidado:** 5 de 5 cenários executados; **15 de 15 asserções aprovadas**; nenhuma falha de asserção nos cinco prints apresentados.

## Registro dos Testes

| ID | Tempo observado | Resposta do serviço | Interpretação |
|---|---:|---|---|
| TC01 | 211 ms | HTTP 200, JSON com `access_token` e `token_type: bearer` | Autenticação válida gerou sessão |
| TC02 | 348 ms | HTTP 400, `error_code: invalid_credentials` | Senha incorreta rejeitada |
| TC03 | 78 ms | HTTP 400, `error_code: invalid_credentials` | Usuário inexistente rejeitado |
| TC04 | 170 ms | HTTP 400, `error_code: validation_failed`, `msg: missing email or phone` | Validação rejeitou campos vazios |
| TC05 | 122 ms | HTTP 400, `error_code: invalid_credentials` | Credenciais inválidas rejeitadas |

Os tempos são os apresentados nas capturas do Postman, não métricas médias ou testes de carga. As cinco respostas foram visualizadas em testes individuais.

A planilha de registro está em `planilha/Registro_Testes_Caixa_Cinza.csv`; os valores representam resultados observados e não simulados. A documentação adicional em `VALIDACAO_TECNICA_POSTMAN.md` separa os testes do aluno de uma execução assistida por monitor.

## Resultados Obtidos

O serviço se comportou como esperado nos cinco cenários. O login válido retornou HTTP 200 com token de acesso. Todas as combinações inválidas foram recusadas com HTTP 400, sem token de acesso. O caso de campos vazios retornou mensagem específica de validação, enquanto os demais cenários inválidos retornaram `invalid_credentials`.

As 15 verificações automáticas do Postman passaram. O retorno HTTP 400, em testes negativos, **não indica falha da aplicação**: foi justamente o comportamento esperado.

**Dificuldade encontrada:** na primeira tentativa no Postman Desktop, o Environment não estava selecionado, o que gerou o erro de resolução de `{{base_url}}` (`getaddrinfo ENOTFOUND`). A seleção correta do ambiente resolveu o problema.

**Limitações:** o exercício avalia apenas uma rota de autenticação e cinco entradas. Não mede desempenho em escala, proteção contra força bruta ou controles avançados de autorização.

## Conclusão

O teste de caixa cinza permitiu validar a autenticação do Supabase conhecendo a estrutura da requisição HTTP, o endpoint, os cabeçalhos e o formato JSON esperado. Os cinco cenários executados no Postman Desktop tiveram comportamento compatível com os requisitos previstos, totalizando 15 verificações aprovadas.

Uma melhoria útil para a rotina de testes seria centralizar variáveis em Environment e manter uma coleção reutilizável com asserções, sem armazenar credenciais em repositórios públicos. Também é importante padronizar evidências com tokens e dados pessoais ocultos.

Os resultados reforçam a utilidade dos testes de caixa cinza em APIs: eles identificam diferenças entre contratos e respostas reais, sem necessidade de uma interface gráfica.

## Evidências e estrutura

Os arquivos abaixo foram conferidos na pasta pública `prints/`:

| Evidência | Arquivo |
|---|---|
| TC01 — Login válido, HTTP 200 e 3/3 testes | [TC1.png](prints/TC1.png) |
| TC02 — Senha incorreta, HTTP 400 e 3/3 testes | [TC2.png](prints/TC2.png) |
| TC03 — Usuário inexistente, HTTP 400 e 3/3 testes | [TC3.png](prints/TC3.png) |
| TC04 — Campos vazios, HTTP 400 e 3/3 testes | [TC4.png](prints/TC4.png) |
| TC05 — Credenciais inválidas, HTTP 400 e 3/3 testes | [TC5.png](prints/TC5.png) |
| Projeto Supabase criado | [01_supabase_projeto.png](prints/01_supabase_projeto.png) |
| Usuário registrado (dados pessoais ocultos) | [02_supabase_auth_usuario.png](prints/02_supabase_auth_usuario.png) |
| Provedor Email habilitado | [02b_supabase_email_habilitado.png](prints/02b_supabase_email_habilitado.png) |

Arquivos de suporte:
- `postman/` — coleção JSON com as cinco requisições e Environment modelo sem credenciais reais.
- `planilha/` — registro dos cinco cenários em Excel e CSV.
- `VALIDACAO_TECNICA_POSTMAN.md` — execução técnica assistida, distinta da execução individual.
- `GUIA_EXECUCAO.md` — procedimentos para reproduzir os testes.

**Evidências complementares ainda não publicadas:** painel das credenciais de API com chave mascarada; Workspace e Environment do Postman; demonstração visual dos headers e body JSON; print da planilha preenchida. Os registros e configurações estão documentados nos arquivos, mas os respectivos prints ainda precisam ser acrescentados para atender integralmente à lista do enunciado.

**Segurança:** nenhuma evidência deve revelar senha, access_token, refresh_token ou chave privada.

## Referências

- Supabase Auth: https://supabase.com/docs/guides/auth/passwords
- Supabase API Keys: https://supabase.com/docs/guides/getting-started/api-keys
- Postman Learning Center: https://learning.postman.com/
- Enunciado fornecido pelo professor: *Atividade Individual — Teste Caixa Cinza com Supabase e Postman*.
