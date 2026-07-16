# Relatório Consolidado de Testes e Melhorias - ArtriApp

Este documento reúne os relatórios de testes, bugs e sugestões identificados para o aplicativo ArtriApp, organizados por membro da equipe.

---

## Gabriel

**Contexto dos Testes:** Testes realizados com o app rodando localmente (build de debug), conectado ao backend também rodando localmente via Docker.

### 1. Bugs Identificados

#### Cadastro
* Não é possível sair da tela de cadastro (sem botão de voltar funcional).
* O cadastro não envia a senha de acesso por e-mail, nada acontece ao clicar em enviar.

#### Diário (Dor, Fadiga, Sono, Inchaço)
* Não é possível salvar o nível de dor: nada acontece ao selecionar o nível e clicar em salvar.
* Ao selecionar várias regiões com dor, não é possível dar scroll na tela. Impede indicar o nível de dor de todas as regiões e impede alcançar o botão de salvar.
* Na tela de Fadiga, o botão "?" não mostra nenhuma informação.
* Não é possível salvar o nível de fadiga.
* Não é possível salvar o nível de sono.
* Na tela de Inchaço, ocorrem os mesmos problemas da tela de Fadiga/Dor: botão "?" não funciona, não é possível salvar o nível de inchaço das regiões, e não é possível dar scroll ao selecionar várias regiões.
* Algumas curiosidades exibidas no menu inicial sofrem overflow de texto dependendo do tamanho do conteúdo.

#### Medicamentos
* O botão para adicionar medicamentos não funciona.
* Não existe botão de voltar na tela de medicamentos.

#### Exercícios
* Nada acontece ao clicar em "Exercícios" no menu inicial.
* No menu "Exercício", o botão "Informações sobre atividades físicas" tem parte do texto cortado.
* Na página de exercícios físicos, o título da página não pode ser lido por completo.
* Na tela de exercícios, parte do texto da dificuldade do exercício é cortado.
* Não é possível assistir aos vídeos em tela cheia. O botão que deveria abrir o modo tela cheia apenas rotaciona a tela, e só é possível desfazer a rotação clicando no botão novamente.
* Ocorre overflow ao tentar abrir alguns vídeos em tela cheia.
* Após algum tempo assistindo aos vídeos, o app fecha inesperadamente.

#### Configurações
* A página de "Alterar e-mail" está quebrada e não possui opção de voltar; clicar em "Home" redireciona para uma página que também está quebrada.
* O mesmo problema ocorre na página de "Alterar Senha".
* O botão "Permissões" não faz nada.

#### Layout Geral
* O app permite uso em modo paisagem, mas não trata o overflow causado por essa orientação.

### 2. Potenciais Problemas

1. **Ausência de tratamento de erros de rede/API na interface:** em vários pontos do app (cadastro, diário, exercícios), quando uma ação falha ou não está implementada, não há nenhum feedback visual (mensagem de erro, loading, etc.) para o usuário, o app simplesmente parece não responder, dificultando diferenciar "travou" de "não fez nada".
2. **Falta de tratamento de estados vazios/sem dados:** telas que dependem de listas vindas do backend (exercícios, treinos) não parecem ter um tratamento visível para quando a resposta vem vazia ou incompleta, o que pode gerar telas em branco ou comportamento inesperado.
3. **Recorrência do mesmo tipo de bug em várias telas** (falta de scroll, botões sem ação, overflow de texto): sugere que esses problemas não são isolados, e sim um padrão de implementação incompleta que provavelmente afeta outras telas não cobertas neste teste.

### 3. Sugestões de Melhoria

1. Implementar tratamento consistente de overflow e scroll (ex.: uso padronizado de `SingleChildScrollView`/`Expanded`/`Flexible`) nas telas que exibem listas de regiões, textos longos ou conteúdo dinâmico, já que esse problema se repete em várias partes do app.
2. Adicionar feedback visual (loading, mensagens de sucesso/erro) para toda ação que dependa de uma resposta do backend (salvar diário, cadastrar, adicionar medicamento), para que o usuário saiba se a ação funcionou, falhou, ou ainda está em andamento.
3. Revisar e completar a navegação entre telas (botões de voltar, redirecionamentos de "Home") nas áreas de Configurações e Medicamentos, garantindo que o usuário sempre tenha uma forma de sair de uma tela sem travar.

---

## Santiago

### 1. Bugs e Potenciais Problemas Identificados

* **Tela de Cadastro:** O botão de voltar não funciona e o gesto nativo de arrastar para a esquerda (swipe) para retornar está inoperante.
* **Gestão de Conta:** Ocorre um problema/falha ao tentar alterar o e-mail do usuário.
* **Tela de Medicamentos:** Não é possível retornar à tela anterior (navegação de volta ausente ou com falha).
* **Tela Inicial:** O botão de "Exercícios" está inativo e não redireciona o usuário para nenhuma tela.
* **Tela de Exercícios (Layout do Título):** O título da tela está truncado. O texto precisa ser responsivo para se adaptar corretamente ao viewport do aparelho.
* **Tela de Exercícios (Layout de Níveis):** Ao acessar os exercícios em qualquer dificuldade, o título e o subtítulo se sobrepõem quebrando o layout do container, e o texto indicativo da dificuldade fica cortado.
* **Tela de Exercícios (Dados):** A duração do exercício está sendo exibida erroneamente como nulls na interface, em vez de exibir um traço (-) ou o valor correto.
* **Player de Vídeo:** Ao maximizar o vídeo dos exercícios, a interface quebra na orientação horizontal e a tela fica travada nessa posição.
* **Ícone de Configurações:** Clicar no ícone de configurações exibe indevidamente a mensagem de saudação "Olá, como você está hoje?".

### 2. Sugestões de Melhoria (UI/UX)

* **Clareza na Seleção de Exercícios:** O texto de instrução está confuso. Atualmente diz "Clique para escolher o nível de dificuldade", mas os botões disponíveis são categorias ("Mãos" e "Pés"). É necessário ajustar o texto para refletir a ação real (ex: "Escolha a categoria do exercício").
* **Otimização do Fluxo de Início:** Inserir um botão de "Avançar/Iniciar" diretamente dentro do Alerta pré-exercício. No fluxo atual, o usuário precisa fechar o alerta (botão "X") e depois clicar em "Começar", gerando cliques e atrito desnecessários.
* **Otimização do Fluxo de Conclusão:** Adicionar um botão explícito (ex: "Voltar para o Menu") abaixo do texto de comemoração ao finalizar um exercício. O uso apenas do botão padrão de voltar gera ambiguidade, dando a impressão de que a ação retornará ao exercício anterior.
* **Acessibilidade Visual:** Melhorar o contraste entre as cores das fontes e os fundos das telas para facilitar a leitura.

---

## Lucas

### 1. Bugs

* Botões redondos não salvam o estado.
* App bar da tela de exercícios cortando o texto.
* Telas dentro do fluxo de configurações não apresentam botão de voltar.
* Engrenagem (switch das configurações) é desabilitado quando entramos em alguma tela dentro do fluxo de configurações.
* Imagem de "Perfil" não corresponde a utilizada no protótipo das telas (essa só é encontrada dentro da tela de alteração de senha).
* Navegação não funciona corretamente em dispositivos android (na maioria das telas).
* Warnings na execução.
* Overflow em dispositivos android nas telas de dor e inchaço.
* Textos desalinhados nos detalhes do exercício.
* Botão com texto cortado (informações sobre atividades físicas).
* Aplicativo crashou com a navegação.
* Aplicativo crashou após clique em link disponibilizado no app.

### 2. Sugestões

* Botão de "exercícios" não funciona (provavelmente o fluxo a ser adicionado).
* Mitos e verdades não estão compatíveis com os protótipos (No app, atualmente, possuímos Botões vermelho e verde, enquanto no protótipo, são palavras "Mito" e "verdade").
* Página de alterar senha não encontrada.
* Página de alterar email não existente.
* Exercícios apresentam lentidão para iniciar os vídeos (provavelmente culpa do pacote utilizado para a reprodução deles).
* Não possui indicativo de senha incorreta.
* Fonte pequena na tela de informações sobre a atividade física.
* Tela de leis e direitos com textos não padronizados (títulos centralizados e títulos não centralizados na mesma página).
* O mesmo ocorre na tela de "sobre o exercício físico".
* O mesmo ocorre em "minha dor".
* Alterar email com problemas (duas imagens de usuário).
* Alterar senha com problemas (duas imagens de usuário).
* Botão de enviar (alterar senha) não segue o figma.
* Botão de permissões não funciona.
* Campos de troca de senha não apresentam formatação de senha.
* Lista de exercícios é mockada (mesmos valores em qualquer nível de dificuldade).

### 3. Sugestões de Features

* Nenhum campo de senha não apresenta botão que habilita visualização da senha inserida.
* Medicamentos não ficam salvos localmente, apresentando loading sempre que entramos na tela.
* Medicamentos não são adicionados a tela de medicamentos.
* Adicionar medicamentos não tem tantas opções quanto no protótipo.
* Envio de troca de email e troca de senha não funcionam.
* Esqueci a senha não funciona.
