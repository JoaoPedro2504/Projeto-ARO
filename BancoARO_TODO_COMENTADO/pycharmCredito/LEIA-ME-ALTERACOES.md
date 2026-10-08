# Banco ARO — integração das funcionalidades de usuários

Base: BancoCreditoARO-main. Código de referência: BancoPycharmLivrosProjeto-main.

Aproveitado e corrigido: validação artesanal de senha forte; verificação de e-mail repetido; senha com bcrypt na inserção e alteração; login; sessão e páginas protegidas; edição dos próprios dados (ID imutável); logout; mensagem Olá, usuário. Também foram corrigidos formulário POST, nomes de campos, nomes da tabela e redirecionamento após login.

A tabela real do banco é USUARIO (singular). Os campos são ID_USUARIO, NOME, EMAIL, SENHA, RECEITA_MENSAL, DESPESA_MENSAL, TIPO_USUARIO. O banco foi preservado.

**Não incluído:** bloqueio após três tentativas, usuário inativo, histórico de três senhas. Essas funções não estavam prontas no projeto de referência e dependem de implementação e ajustes no banco. Não foi possível comprovar equivalência com o Figma. A home criada é básica, não o painel financeiro final.

## Como iniciar

Instale dependências: `pip install -r requirements.txt`. Instale/inicie Firebird e configure `ARO_DB_PATH` para o caminho absoluto de BANCO.FDB, `ARO_DB_PASSWORD`, `ARO_DB_USER` e `ARO_SECRET_KEY` (chave aleatória forte); então execute `python main.py` dentro de pycharmCredito.

As telas e imagens originais foram preservadas; imagens existentes também foram copiadas para Static/img.

Antes de produção: configurar credenciais e SECRET_KEY seguras e HTTPS, proteção CSRF, limitação de tentativas e revisar textos promocionais de criptografia.
