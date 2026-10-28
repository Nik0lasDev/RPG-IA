# Crônicas — RPG de mesa

RPG narrativo de fantasia que roda diretamente no navegador. Crie um personagem, distribua atributos, escolha classe e talentos, escreva suas próprias ações e deixe os dados resolverem os momentos incertos.

## Jogar

- Abra o arquivo `index.html` localmente, ou publique o repositório com GitHub Pages.
- O jogo salva o progresso automaticamente neste navegador.
- Use **Exportar save** para baixar uma cópia em JSON e **Importar save** para restaurá-la em outro navegador ou dispositivo.

## Sistemas implementados

- **Criação de personagem:** seis classes, cinco origens, atributos distribuídos por pontos, passado opcional e duas habilidades iniciais.
- **Ações livres:** escreva intenções com suas próprias palavras. O jogo interpreta categorias de ação, escolhe o atributo apropriado e resolve um teste.
- **Dados:** D2 para decisões binárias, D6 para acontecimentos rápidos, D20 para testes de ação e D100 para chances percentuais. Os dados também podem ser rolados manualmente.
- **Combate por turnos:** atacar, usar magia, defender/esquivar, tentar negociar ou fugir; inimigos causam dano e oferecem recompensas.
- **Campanhas diferentes:** quatro tons de campanha, sementes e objetivos principais com etapas, além de locais, rumores, encontros e personagens.
- **Progressão:** experiência, níveis, atributos, energia, vida, ouro e inventário.
- **Pós-jogo contínuo:** após concluir o objetivo principal, o jogo passa a gerar contratos, encontros e situações recorrentes. O personagem pode continuar subindo de nível e treinar atributos com mentores.
- **Persistência local:** o progresso fica em `localStorage`, com exportação e importação manual.

## Controles

- **O que você faz?** Digite uma ação livre ou escolha uma sugestão.
- **Dados de mesa:** clique em D2, D6, D20 ou D100 para rolar o dado.
- **Ficha do herói:** consulte atributos, habilidades e recursos.
- **Explorar o mundo:** viaje para outras regiões e encontre novas situações.
- **Descansar:** recupera vida e energia, avançando o tempo.

## Publicar no GitHub Pages

O repositório inclui um workflow em `.github/workflows/pages.yml` para publicar os arquivos estáticos ao enviar commits para `main`. Em **Settings → Pages**, selecione **GitHub Actions** como fonte de publicação. O GitHub Pages hospeda arquivos estáticos; o jogo não requer servidor nem dependências de build.

A URL esperada do projeto é:

https://nik0lasdev.github.io/RPG-IA/

## Mestre com IA generativa (opcional)

O jogo agora pode usar um modelo de linguagem compatível com a API de **chat completions** para narrar cenas com mais contexto, interpretar a intenção do jogador, manter fatos recorrentes da campanha e sugerir ações coerentes. O sistema de regras local continua controlando atributos, testes, combate, vida, inventário e recompensas; a IA não deve inventar alterações mecânicas.

1. Inicie uma campanha e abra **Mestre IA** no cabeçalho da tela de jogo.
2. Informe o endpoint HTTPS do provedor, o identificador do modelo e sua chave de API.
3. Clique em **Testar conexão** e, se funcionar, em **Ativar mestre IA**.
4. Faça ações normalmente. A IA interpreta a intenção antes da resolução e depois devolve narração, três sugestões e atualizações de memória estruturada.

O endpoint inicial é o da OpenRouter e o modelo sugerido é `openai/gpt-4o-mini`; ambos podem ser alterados para outro provedor/modelo compatível. O provedor escolhido precisa permitir chamadas do navegador via CORS e aceitar o formato de chat completions. Uso de API pode gerar custos cobrados pelo provedor.

### Memória persistente da campanha

A campanha mantém um **cronicário estruturado** no save local, em vez de depender apenas das últimas mensagens. Ele organiza:
- resumo canônico da história;
- NPCs, facções, locais, objetos e ameaças recorrentes;
- relações entre personagens, alianças, rivalidades e mudanças de estado;
- fatos, pistas, promessas, dívidas e informações com grau de certeza;
- fios narrativos abertos, em andamento, resolvidos ou abandonados;
- linha do tempo dos turnos e resultados registrados pelo jogo.

A cada turno, o jogo registra a ação e as consequências mecânicas na linha do tempo. Quando a IA está ativa, ela também atualiza entidades, relações, fatos e tramas; antes de narrar, recebe uma seleção de memórias relevantes, o resumo canônico e os acontecimentos recentes. Saves antigos são migrados automaticamente para a nova estrutura, e o cronicário acompanha a exportação/importação do save.

A memória é limitada por categoria para controlar o tamanho do contexto, mantendo um resumo e registros recentes. Como o jogo é estático, o cronicário fica no navegador e **não sincroniza automaticamente entre dispositivos**. Exporte o save para fazer backup ou transferi-lo. Nenhum modelo garante lembrança perfeita: a qualidade depende do modelo, do contexto disponível e das respostas produzidas. Para maior privacidade e confiabilidade em uso público, um backend com banco de dados e validação no servidor seria o próximo passo.

### Segurança da chave

A chave não é gravada no repositório nem no save do jogo: fica em `sessionStorage`, para a sessão atual do navegador. Ainda assim, uma chave usada no navegador pode ser acessada por extensões ou scripts executados na página. Use uma chave com limite de gastos e permissões mínimas. **Para publicar o jogo para outras pessoas, a solução recomendada é um backend próprio**, com a chave guardada no servidor e limites de uso. Não coloque chaves secretas em arquivos JavaScript ou no GitHub Pages.

Sem chave ou quando o provedor estiver indisponível, o jogo continua funcionando com o mestre local.

## Desenvolvimento

Sem dependências externas de JavaScript. Estrutura:
- `index.html` — estrutura da interface
- `styles.css` — estilo responsivo
- `game.js` — regras, narrativa, dados, combate e salvamento
- `.github/workflows/pages.yml` — publicação no GitHub Pages