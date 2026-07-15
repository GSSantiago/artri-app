# ArtriApp - Lista de Bugs, Potenciais Problemas e Sugestões de Melhoria

Testes realizados com o app rodando localmente (build de debug), conectado ao backend também rodando localmente via Docker.

## 1. Bugs Identificados

### Cadastro
- Não é possível sair da tela de cadastro (sem botão de voltar funcional).
- O cadastro não envia a senha de acesso por e-mail, nada acontece ao clicar em enviar.

### Diário (Dor, Fadiga, Sono, Inchaço)
- Não é possível salvar o nível de dor: nada acontece ao selecionar o nível e clicar em salvar.
- Ao selecionar várias regiões com dor, não é possível dar scroll na tela. Impede indicar o nível de dor de todas as regiões e impede alcançar o botão de salvar.
- Na tela de Fadiga, o botão "?" não mostra nenhuma informação.
- Não é possível salvar o nível de fadiga.
- Não é possível salvar o nível de sono.
- Na tela de Inchaço, ocorrem os mesmos problemas da tela de Fadiga/Dor: botão "?" não funciona, não é possível salvar o nível de inchaço das regiões, e não é possível dar scroll ao selecionar várias regiões.
- Algumas curiosidades exibidas no menu inicial sofrem overflow de texto dependendo do tamanho do conteúdo.

### Medicamentos
- O botão para adicionar medicamentos não funciona.
- Não existe botão de voltar na tela de medicamentos.

### Exercícios
- Nada acontece ao clicar em "Exercícios" no menu inicial.
- No menu "Exercício", o botão "Informações sobre atividades físicas" tem parte do texto cortado.
- Na página de exercícios físicos, o título da página não pode ser lido por completo.
- Na tela de exercícios, parte do texto da dificuldade do exercício é cortado.
- Não é possível assistir aos vídeos em tela cheia. O botão que deveria abrir o modo tela cheia apenas rotaciona a tela, e só é possível desfazer a rotação clicando no botão novamente.
- Ocorre overflow ao tentar abrir alguns vídeos em tela cheia.
- Após algum tempo assistindo aos vídeos, o app fecha inesperadamente.

### Configurações
- A página de "Alterar e-mail" está quebrada e não possui opção de voltar; clicar em "Home" redireciona para uma página que também está quebrada.
- O mesmo problema ocorre na página de "Alterar Senha".
- O botão "Permissões" não faz nada.

### Layout Geral
- O app permite uso em modo paisagem, mas não trata o overflow causado por essa orientação.

## 2. Potenciais Problemas

1. **Ausência de tratamento de erros de rede/API na interface**: em vários pontos do app (cadastro, diário, exercícios), quando uma ação falha ou não está implementada, não há nenhum feedback visual (mensagem de erro, loading, etc.) para o usuário, o app simplesmente parece não responder, dificultando diferenciar "travou" de "não fez nada".
2. **Falta de tratamento de estados vazios/sem dados**: telas que dependem de listas vindas do backend (exercícios, treinos) não parecem ter um tratamento visível para quando a resposta vem vazia ou incompleta, o que pode gerar telas em branco ou comportamento inesperado.
3. **Recorrência do mesmo tipo de bug em várias telas** (falta de scroll, botões sem ação, overflow de texto): sugere que esses problemas não são isolados, e sim um padrão de implementação incompleta que provavelmente afeta outras telas não cobertas neste teste.

## 3. Sugestões de Melhoria

1. Implementar tratamento consistente de overflow e scroll (ex.: uso padronizado de `SingleChildScrollView`/`Expanded`/`Flexible`) nas telas que exibem listas de regiões, textos longos ou conteúdo dinâmico, já que esse problema se repete em várias partes do app.
2. Adicionar feedback visual (loading, mensagens de sucesso/erro) para toda ação que dependa de uma resposta do backend (salvar diário, cadastrar, adicionar medicamento), para que o usuário saiba se a ação funcionou, falhou, ou ainda está em andamento.
3. Revisar e completar a navegação entre telas (botões de voltar, redirecionamentos de "Home") nas áreas de Configurações e Medicamentos, garantindo que o usuário sempre tenha uma forma de sair de uma tela sem travar.
