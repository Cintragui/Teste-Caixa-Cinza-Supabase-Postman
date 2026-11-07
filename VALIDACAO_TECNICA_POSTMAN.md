# Validação técnica assistida — Postman Monitor

**Este registro é distinto dos cinco testes realizados pelo aluno no Postman Desktop.**

- **Ferramenta:** Postman Monitor (execução manual via integração)
- **Monitor:** VALIDACAO TECNICA TC02-TC05 - Caixa Cinza
- **Status do monitor:** Inativo; não foi deixada execução recorrente.
- **Data:** 07/11/2026
- **Execução:** 16:14:35Z a 16:14:37Z
- **Resultado reportado:** success
- **Requisições:** 4, com 0 falhas
- **Asserções:** 12, com 0 falhas
- **Cenários:** TC02, TC03, TC04 e TC05
- **HTTP observado:** 400 nos quatro cenários.

| Cenário | HTTP | Asserções |
|---|---:|---:|
| TC02 — Senha incorreta | 400 | 3/3 |
| TC03 — Usuário inexistente | 400 | 3/3 |
| TC04 — Campos vazios | 400 | 3/3 |
| TC05 — Credenciais inválidas | 400 | 3/3 |

O login válido TC01 **não** foi executado via monitor por não haver senha correta na integração. O aluno executou TC01 e os demais casos separadamente no Postman Desktop, com cinco capturas mostrando 15/15 asserções aprovadas.

Este arquivo serve à rastreabilidade técnica, não substitui os prints reais do aluno.
