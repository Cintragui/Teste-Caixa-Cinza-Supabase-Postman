# Guia de reprodução dos testes

O Workspace pessoal **Teste Caixa Cinza - Supabase**, a coleção e o Environment foram criados no Postman conectado à conta do aluno.

1. Abra o **Postman Desktop** com a conta na qual os recursos foram criados.
2. Abra o Workspace **Teste Caixa Cinza - Supabase**.
3. Selecione o Environment **Supabase - Caixa Cinza - Testes** (no canto superior direito).
4. Verifique `base_url` e `api_key`. Preencha a variável `password` **somente no valor local**, sem sincronizar nem compartilhar. O e-mail também deve ser mantido fora do repositório.
5. Abra e envie cada requisição de TC01 a TC05.
6. Na resposta, anote o **HTTP**, tempo, o campo `error_code` ou a existência de token e os resultados na aba **Test Results**.
7. **Nunca** copie o valor de `access_token`, `refresh_token`, senhas ou chaves para screenshots, documentos ou commits.
8. Salve as cinco capturas de execução na pasta `prints/`.
9. Para o relatório do professor, registre também os prints de configuração do Supabase (projeto, Auth, usuário, API Keys mascaradas), e do Postman (Workspace, Environment, Headers, Body).
10. Se republicar a coleção, exporte **somente** variáveis de exemplo, não o Environment preenchido.

## Falha corrigida durante a atividade

Ao abrir o Postman Desktop inicialmente, não havia Environment selecionado. Isso causou `getaddrinfo ENOTFOUND {{base_url}}`. Selecionar o Environment correto resolveu o problema.

## Interpretação dos erros HTTP

O HTTP 400 em TC02 a TC05 é o comportamento esperado; a rejeição de credenciais inválidas é exatamente o resultado testado. Um teste só é aprovado quando as verificações de conteúdo e status passam.

## Relação com o GitHub e o Supabase

O GitHub hospeda a documentação e os arquivos de teste. **Não é necessário conectar o repositório ao Supabase** para executar os testes desta atividade. A API de autenticação permanece hospedada pelo Supabase e é acessada pelo Postman.
