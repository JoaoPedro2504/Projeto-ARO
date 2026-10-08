# Segurança adicionada ao Banco ARO

Requisitos implementados no código:
- Bloqueio permanente por usuário após 3 senhas erradas; tentativas ficam na tabela USUARIO. Login válido zera as tentativas antes do bloqueio.
- Usuário inativo (ATIVO=0) não faz login nem acessa páginas protegidas.
- Nova senha não pode coincidir com a senha atual nem com as 3 anteriores, comparadas por bcrypt; histórico conserva apenas os hashes anteriores.

## Banco Firebird
Execute `python main.py` com o Firebird ativo e com conta autorizada a alterar o esquema. A função `preparar_seguranca()` cria os campos ATIVO, TENTATIVAS_LOGIN e BLOQUEADO na tabela USUARIO e a tabela HISTORICO_SENHA, somente se não existirem. Faça backup do BANCO.FDB antes da primeira execução.

Para inativar manualmente uma conta (com permissão de administrador do banco):
`UPDATE USUARIO SET ATIVO = 0 WHERE ID_USUARIO = 123; COMMIT;`
Para reativar e desbloquear após verificar a identidade do usuário:
`UPDATE USUARIO SET ATIVO = 1, BLOQUEADO = 0, TENTATIVAS_LOGIN = 0 WHERE ID_USUARIO = 123; COMMIT;`
Substitua 123 pelo ID correto. Não foi adicionada uma tela administrativa de desbloqueio.

IMPORTANTE: para usuários antigos, as senhas anteriores à primeira troca não são recuperáveis, então a regra passa a ser aplicada prospectivamente. Recomendado adicionar proteção CSRF e rate-limit por IP antes de publicar.
