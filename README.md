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

## Limites atuais

A interpretação de texto é feita por regras locais e palavras-chave; não usa um modelo de IA externo nem requer chave de API. As respostas são narrativas procedurais, não um mestre de mesa generativo de linguagem natural. O pós-jogo pode continuar indefinidamente através de contratos e situações combinadas, mas o conteúdo é gerado a partir de conjuntos e regras do próprio jogo.

## Desenvolvimento

Sem dependências externas de JavaScript. Estrutura:
- `index.html` — estrutura da interface
- `styles.css` — estilo responsivo
- `game.js` — regras, narrativa, dados, combate e salvamento
- `.github/workflows/pages.yml` — publicação no GitHub Pages