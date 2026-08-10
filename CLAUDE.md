# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Regras invioláveis

1. **O PDF tem no máximo 2 páginas.** Não é preferência, é requisito. Nenhuma edição do `.tex` está concluída antes de o log confirmar `(2 pages)`. Se a mudança estourar para 3, **corte algo** (ver Orçamento de espaço) — nunca entregue 3 páginas nem reduza fonte/margem para disfarçar.
2. **O PDF é recompilado a cada alteração do `.tex`.** Ele é entregável versionado; o git não sabe que deriva da fonte. Já aconteceu de um PDF defasado distribuir um claim que havia sido suavizado.
3. **O `.tex` é a fonte da verdade.** Onde `.tex` e `README.md` discordarem sobre um **fato** (empresa, cargo, período, métrica, claim técnico), o `.tex` está certo e o README é que se corrige — nunca o contrário. Se o `.tex` estiver factualmente errado, o conserto é editar o `.tex` **primeiro** e propagar para o README depois, nessa ordem. Isso não apaga a divergência legítima de **profundidade**: o README continua podendo detalhar o que o `.tex` cortou por espaço.
4. **Nada que ultrapasse o teto de claims** (camada 1 em Regras de conteúdo) **entra sem que o conflito seja apontado ao Leandro primeiro**, com o limite nomeado e a alternativa defensável na mesa. A decisão final é dele; o que não pode acontecer é ele descobrir na entrevista.

## O que é este repositório

Não é um projeto de software: é o **currículo do Leandro Rocha de Brito** (Desenvolvedor Mobile Flutter Sênior) mantido como código. O conteúdo vive em dois artefatos:

| Arquivo | Papel | Público |
|---|---|---|
| `curriculo-leandro-rocha-flutter.tex` | PDF de candidatura, otimizado para ATS | recrutador / robô de triagem |
| `README.md` | perfil do GitHub | quem chega pelo link do GitHub |

**Eles divergem de propósito, e a divergência é bidirecional.** O `.tex` tem orçamento rígido de 2 páginas; o README não tem limite, mas também não foi atualizado em todas as revisões. Divergências conhecidas hoje:

- **Só no README:** experiência da EULABS, contagem de avaliações da Play Store (17.6K, 58.7K), nota do iOS, ementa detalhada do MBA, o bullet `Integrações e infraestrutura mobile` da Clyvo e a separação de `Teleconsulta` e `Onboarding` em dois bullets (o `.tex` funde por espaço), `hipóteses diagnósticas` e o documento de `alta` no projeto da Clyvo, `GitHub Actions` nomeado no Lions Pontos.
- **Só no `.tex`:** nada nas Habilidades — a lista foi sincronizada em Agosto/2026 e as duas devem permanecer idênticas.
- **As Apresentações são textos distintos, não versões do mesmo.** A do README abre com `6 anos de experiência em desenvolvimento de software`, que não existe no `.tex`. Não presuma que estão sincronizadas: leia as duas antes de editar qualquer uma.

Ao alterar um **fato** (empresa, período, métrica, claim), atualize os dois — sempre no sentido `.tex` → `README.md` (regra inviolável nº 3). Ao alterar **profundidade** (cortar por espaço, detalhar), só o arquivo em questão.

Divergência de fato entre os dois arquivos é **defeito, não escolha editorial**: recrutador cruza PDF, README e LinkedIn, e um período que não bate vira pergunta na entrevista. Ao encontrar uma, não escolha sozinho qual versão vale — o `.tex` é a referência, mas se o conflito sugerir que o próprio `.tex` está errado (ex.: dois empregos com datas que não encaixam), pergunte ao Leandro antes de propagar.

`temp/` é área de trabalho ignorada pelo git (respostas de entrevista, requisitos de vagas, gaps/roadmap). Serve de contexto, não é entregável — e é o lugar de qualquer lista volátil (backlog de ajustes, blocos a revisar), que não deve entrar neste arquivo.

## Fluxo de trabalho

Ao mudar conteúdo do currículo:

1. **Cheque o teto antes de escrever.** Leia a camada 1 (Fato) e confirme que o projeto em questão sustenta o que será afirmado.
2. **Edite o `.tex`.** Aplique as camadas 2 e 3 na redação.
3. **Recompile** (duas passadas) e confirme `(2 pages)` no log. Estourou? Volte ao Orçamento de espaço.
4. **Extraia o texto do PDF** e confira a integridade da extração ATS.
5. **É fato? Atualize o `README.md` também.** É só profundidade? Fica no arquivo editado.
6. **Não commite sem pedir.** Deixe as mudanças no working tree e relate o que mudou.

## Build do PDF

O TeX Live instalado é o **BasicTeX**, que **não tem `latexmk`**. O documento usa `fontspec` + fonte Inter do sistema, então **exige `xelatex`** — `pdflatex` não carrega fontes OpenType do sistema.

```bash
# duas passadas: a 1ª gera .aux/.out, a 2ª estabiliza os bookmarks do hyperref
xelatex -interaction=nonstopmode -file-line-error -output-directory=build curriculo-leandro-rocha-flutter.tex
xelatex -interaction=nonstopmode -file-line-error -output-directory=build curriculo-leandro-rocha-flutter.tex
mv -f build/curriculo-leandro-rocha-flutter.pdf .
```

**A raiz do repositório contém apenas o `.tex` e o `.pdf`.** Todo auxiliar (`.aux`, `.log`, `.out`, `.xdv`) fica em `build/`, ignorado pelo git. Se algum auxiliar aparecer na raiz, foi build rodado sem `-output-directory` — apague.

SyncTeX está desligado de propósito (sem `-synctex=1`): o `.synctex.gz` só funciona ao lado do PDF, e mantê-lo na raiz contraria a regra acima. Para reativar, acrescente a flag e volte a mover o `.synctex.gz` junto com o PDF.

No VSCode, a receita equivalente (`xelatex ×2 → raiz`) está em `.vscode/settings.json`, com as justificativas de cada flag comentadas ali. `autoBuild` está desligado — o build é manual.

### Verificação após editar o `.tex`

**1. Duas páginas** (regra inviolável nº 1):

```bash
grep 'Output written' build/curriculo-leandro-rocha-flutter.log   # precisa dizer "(2 pages)"
```

**2. Extração ATS íntegra.** **Não há `pdftotext` nesta máquina** (sem poppler) nem PyObjC/Quartz no Python do sistema; o caminho que funciona é PDFKit via Swift:

```bash
cat > /tmp/pdftxt.swift <<'EOF'
import Foundation
import PDFKit
let d = PDFDocument(url: URL(fileURLWithPath: CommandLine.arguments[1]))!
for i in 0..<d.pageCount { print("=== PAGINA \(i+1) ==="); print(d.page(at: i)?.string ?? "") }
EOF
swift /tmp/pdftxt.swift curriculo-leandro-rocha-flutter.pdf
```

No texto extraído, confira: parênteses e hífens presentes (`(FaceTec)`, `multi-tenant`), `PJ` sem espaço no meio, `fl_chart` e `build_runner` inteiros, e a ordem de leitura acompanhando o documento.

## Orçamento de espaço

Acréscimo de ~3 linhas já estoura para 3 páginas. Quando algo novo precisa entrar, **abra espaço antes de escrever** — não depois de descobrir que não coube. Candidatos a corte, do mais fraco para o mais forte:

1. **Item que não passa no teste de over-engineering** (ver seção abaixo) — sai primeiro, porque cortá-lo melhora o texto além de abrir espaço.
2. **Contagem bruta** — `19 migrations` já saiu por isso; se aparecer outra, é a próxima.
3. **Bullet que é só lista de tecnologia sem efeito** — o `Integrações e infraestrutura mobile` da Clyvo saiu assim; as tecnologias já estavam em Habilidades.
4. **Descrições de empresa** — podem encolher para meia linha; o recrutador conhece Claro e Monetizze.
5. **URLs de empresa no `\job`** — são metadado de verificação, não conteúdo.

Fundir dois bullets economiza mais que encurtar duas frases: o ambiente `tight` cobra `itemsep` e recuo **por item**, não por linha de texto.

O que **nunca** é cortado para ganhar espaço: o "antes" de uma métrica de impacto, o alcance de uma entrega (`adotado pelo time`), qualquer coisa da seção Habilidades que dê match de keyword no ATS, e o título e a Apresentação (ver "O topo carrega o maior peso") — o topo é a última coisa a ceder, porque é o que decide se o resto será lido.

Também nunca reduza corpo de fonte, entrelinha ou margem para caber. O documento já está calibrado em 9pt / 1.12 / 1.35cm; apertar mais prejudica a leitura humana, que é quem decide.

## Calibração para uma vaga

Quando houver um arquivo de requisitos de vaga em `temp/`, ele é o alvo:

1. **Extraia o vocabulário do job description** — tecnologias, práticas e o nome que a empresa dá ao papel (ex.: "referência técnica").
2. **Cruze com o título, as Habilidades e o `pdfkeywords`.** Termo que ele domina mas o currículo não nomeia é ganho fácil: acrescente com a grafia usada na vaga. O título abaixo do nome é o ajuste de maior retorno (ver "O topo carrega o maior peso").
3. **Só entra o que é verdade.** Gap real se reporta ao Leandro; não se preenche. Ver regra inviolável nº 4.
4. **Reordene, não invente.** Se a vaga enfatiza testes, o bloco de qualidade sobe dentro da experiência. A ordem é ajuste barato e legítimo.

## Decisões ATS-safe — não alterar sem revalidar a extração

O `.tex` carrega escolhas que existem só para o texto sair íntegro do extrator do ATS. Estão comentadas no topo do arquivo; o resumo do porquê:

- **Coluna única, sem tabelas de layout, sem ícones.** Layout em duas colunas embaralha a ordem de leitura na extração.
- **Contato no corpo do documento, nunca em header/footer.** Muitos parsers descartam header e footer.
- **`Ligatures={NoCommon,NoContextual}`** — sem isso "fi"/"fl" viram um glifo só e quebram a palavra na extração.
- **`RawFeature={-calt;-case}`** — as alternativas contextuais da Inter substituem `(`, `)` e `-` por glifos sem mapeamento ToUnicode; parênteses e hífens simplesmente somem do texto extraído.
- **Fonte `\nokern`** (com `-kern`) para trechos curtos com par de glifos de kerning forte, hoje usada em `PJ`. O xdvipdfmx grava o kern como deslocamento no operador `TJ` e o extrator lê como espaço → sai `P J`. Se um novo trecho sair partido na extração, é candidato a `\nokern`.
- **Hifenização desligada** (`\hyphenpenalty=10000`): palavra partida no fim da linha não dá match de keyword.
- **`\hypersetup{pdfkeywords=...}`** — alguns ATS leem os metadados do PDF antes de extrair o corpo. Ao acrescentar uma tecnologia relevante nas Habilidades, reflita em `pdfkeywords`.

Consequência de legibilidade: como não há hifenização, o texto é **ragged right** (`\raggedright`) — justificar sem hifenizar produz rios brancos.

## Paleta e comandos do `.tex`

Quatro tons derivados de `#120A8F`, todos abaixo de 36% de luminância para não sumirem em impressão P&B: `ink` (texto), `accent` (nome/seções/empresas), `rule` (filetes/marcadores), `muted` (rótulos/metadados).

Macros: `\sect{}` (título de seção), `\job{empresa}{cargo}{vínculo}{período}{url}`, `\fld{}` (rótulo discreto: "Descrição da Empresa", "Projeto"), `\lbl{}` (rótulo dentro de bullet), ambiente `tight` (lista compacta, sem depender de `enumitem`).

---

# Regras de conteúdo

Estas restrições vieram do próprio Leandro, já validadas, e valem mais que qualquer sugestão genérica de redação de currículo.

São três camadas, **nesta ordem de precedência**. Elas aparecem abaixo na mesma ordem. **Nunca resolva um conflito subindo de camada:**

1. **Fato** — teto rígido. O que aconteceu é imutável.
2. **Posicionamento** — o ângulo com que o fato é contado. Age só dentro do teto.
3. **Estilo** — o registro da frase.

## 1. Fato — limites de claims

Não reintroduzir como conquista dele:

- **Nunca liderou formalmente** (sem tech lead, sem mentoria formal). A senioridade é técnica.
- **Claro Pay / Amaris:** implementou spec pronta. Não concebeu o módulo nem decidiu a arquitetura de microapps.
- **Clyvo:** o assistente de IA por voz é de outra pessoa. WebRTC/LiveKit e CallKit/IncomingCall ele **refatorou o que já existia** — nas Experiências, entra como "manutenção e evolução", nunca como autoria. **Em Habilidades, decisão dele (Agosto/2026): listar direto, sem ressalva**, depois de ouvir a objeção. Não reabra; o lastro para a entrevista é refatoração, não implementação inicial. Não há CI no mobile. Não há pagamento in-app. `apps/vet` está vazio, não é um segundo app.
- **Clyvo — o que é dele, e pode ser afirmado com força:** conduziu a migração multirepo → monorepo (Dart Workspace, 31 módulos); pegou uma base sem nenhum teste e a levou a 6.800 testes e 85% de cobertura, definindo a estratégia e os padrões do time; introduziu a prática de code review no time mobile; biometria facial e OCR de documentos (FaceTec — **não usar ML Kit**, corrigido por ele em Agosto/2026); assinatura digital com PDF; design system e SDK de chat; monitoramento e investigação de incidentes em produção com Datadog e Crashlytics.
- **Lions Pontos:** projeto pessoal, autoria total. Único lugar onde ele pode reivindicar tudo, inclusive o CI.
- **Inglês:** técnico (leitura), não conversação.

Não deduza funcionalidade de árvore de pastas nem de nome de módulo sem confirmar com ele. Currículo inflado quebra na primeira pergunta de follow-up, e a desconfiança em um item contamina o documento inteiro.

### Quando um pedido ultrapassa o teto

Acontece de o pedido ser legítimo na intenção ("quero soar mais sênior") e ultrapassar o teto na formulação. Não obedeça nem recuse seco. **Nomeie o limite específico, e ofereça a formulação defensável mais forte:**

> "Isso reivindicaria liderança formal, que não houve. O mais forte que o fato sustenta é `introduzi a prática de code review no time mobile` — que já prova influência sobre o time, sem cargo."

Se ele reafirmar depois de ouvir a objeção, é decisão dele: diga a ressalva em uma frase, na conversa, e aplique. Não insista, não repita o argumento e não deixe comentário de ressalva no `.tex`.

## 2. Posicionamento — o que o texto precisa provar

Cada bloco tem que deixar quatro impressões: **competência técnica**, **entrega de resultado e valor para o negócio**, **protagonismo** e **autonomia**.

### São dois leitores, e o texto precisa servir aos dois

O currículo passa por duas pessoas com critérios opostos, e um texto escrito para uma só é reprovado pela outra:

| Leitor | O que procura | Reprova quando |
|---|---|---|
| **RH / recrutador não técnico** — filtra primeiro | palavras da vaga, empresas, tempo, e uma frase que ele entenda sobre o que mudou | o texto é jargão puro e ele não consegue avaliar nem repassar |
| **Tech lead** — avalia depois | decisão técnica com motivo, escala real, sinais de que a pessoa sabe o que **não** fazer | vê tecnologia empilhada sem problema que a justifique |

**A regra que atende aos dois: cada item traz o problema, a escolha e o efeito.** O RH entende o problema e o efeito; o tech lead avalia a escolha. Uma frase, três funções:

> `como cada clube só pode ver os próprios dados, o isolamento é garantido por Row Level Security no banco e não na aplicação`

O RH lê "cada clube só vê os próprios dados". O tech lead lê "RLS no banco, não na aplicação" e reconhece a decisão certa. Ninguém precisou de duas versões do texto.

### Nada de over-engineering

**Tecnologia sofisticada sem problema declarado lê como over-engineering, e over-engineering é sinal de imaturidade técnica** — exatamente o oposto do que se quer provar. O tech lead não pergunta "usou o que há de mais moderno?", pergunta "essa complexidade se pagou?".

Antes de manter qualquer item sofisticado no currículo, ele precisa passar nos três:

1. **Qual problema real resolvia?** Se não há problema declarado, corte o item.
2. **Por que essa escolha e não a simples?** A justificativa entra no texto, curta, no lugar do jargão.
3. **Deu resultado?** Com antes/depois de impacto onde ele existir, sem inventar magnitude.

Não passou nos três: **corte, mesmo que seja verdade.** Item verdadeiro que parece exagero custa mais do que rende — e é o primeiro lugar onde procurar espaço quando o PDF estourar as 2 páginas.

Atenção especial ao **Lions Pontos**: é projeto voluntário e todo rigor ali (multi-tenant, RLS, cobertura alta, CI barrando merge) parece desproporcional se o motivo não estiver escrito ao lado. Escrito o motivo — dados de clubes não podem se misturar, o ranking define um prêmio e erro de cálculo não é aceitável — o mesmo rigor lê como julgamento. **A justificativa é o que separa "over-engineering" de "critério".**

O eixo é **raio de impacto, não cargo**: senioridade se lê em entregas que mudam como o time ou o produto funciona, e em decisões tomadas sob incerteza. Leandro nunca teve cargo de liderança e isso não é obstáculo — vaga de dev sênior mede influência técnica, não gestão de pessoas.

### Como escrever

- **Ele é o sujeito da frase, com verbo de entrega.** Evite o passivo e o vago: `Atuei na`, `Participei de`, `Contribuí para`, `Fui responsável por`, `Trabalhei com`.
- **O verbo é escolhido pelo objeto, não por lista.** Nenhum verbo é bom ou mau isolado — o que decide é se o fato daquele projeto o sustenta. `Estruturei os 31 módulos com Clean Architecture` é verdade na Clyvo; `estruturei o projeto` seria falso na Amaris. Antes de escolher o verbo, confira o teto na camada 1.
- **Onde o teto não permite autoria, use a formulação defensável mais forte** (`desenvolvimento end-to-end`, `implementei o módulo dentro da arquitetura adotada`), nunca recue para o passivo. Currículo inflado quebra na entrevista; currículo tímido não chega até ela.
- **Explicite o alcance quando ele passa do próprio código.** `adotado pelo time`, `introduzi no time mobile`, `compartilhado entre os apps do monorepo`. É assim que protagonismo aparece sem reivindicar cargo.
- **Agência explícita: quem decidiu, decidiu.** O erro mais comum é narrar como se a coisa tivesse acontecido sozinha ou como se o time tivesse feito — `foi adotado`, `a base chegou a 6.800 testes`, `o padrão passou a ser`. Substantivo abstrato (`concepção e desenvolvimento`) esconde o autor tanto quanto voz passiva; use o verbo (`concebi e desenvolvi`). Quando ele propôs, convenceu ou enfrentou resistência, isso é conteúdo, não bastidor: `propus`, `defendi`, `convenci o time a`, `assumi a decisão de` valem mais que qualquer adjetivo, porque descrevem influência com um fato por trás. Confira o teto na camada 1 antes.
- **Feche o arco: o que fez → o que mudou.** Tecnologia sozinha descreve tarefa; tecnologia + efeito descreve entrega. `Utilizei TDD para garantir robustez` é fraco; `Entreguei o módulo end-to-end com TDD` é entrega.
- **Traduza o técnico em valor de negócio onde houver.** Cobertura de teste vira risco de regressão; monorepo vira atrito entre times; multi-tenant vira isolamento de dados entre clientes. Sem virar frase de efeito comercial (camada 3).
- **Autonomia se prova com escopo, não com adjetivo.** `do modelo de dados ao deploy`, `único responsável pelas decisões técnicas` valem mais que "profissional autônomo e proativo". Nunca use auto-elogio: `proativo`, `apaixonado por tecnologia`, `visão sistêmica`, `excelente comunicação`. Recrutador desconta o que o candidato diz de si mesmo e só credita o que ele demonstra.

### O topo carrega o maior peso

**Título e Apresentação decidem se o resto é lido.** Ocupam o primeiro terço da primeira página, estão no topo do que o parser do ATS indexa, e o recrutador passa segundos ali antes de escolher entre continuar e ir para o próximo currículo. Regras próprias:

- **O título abaixo do nome deve espelhar o cargo da vaga**, quando for verdade. `Desenvolvedor Mobile Flutter Sênior` casa com "Desenvolvedor Flutter Sênior"; se a vaga escreve "Engenheiro de Software Mobile", vale ajustar. É o campo de maior peso em boa parte dos ATS. Nunca invente um nível acima do que ele tem.
- **A Apresentação tem 3 a 4 linhas.** Não é resumo do currículo, é o argumento de por que continuar lendo. Mantê-la enxuta é escolha editorial, não economia de espaço: se ela crescer, o excedente vai para a experiência correspondente — e nunca se corta o topo para abrir espaço em outro lugar.
- **Ordem do que entra**, do mais forte para o mais fraco: (1) o que ele é e há quanto tempo em Flutter — é filtro duro de ATS e de recrutador, precisa estar lá; (2) o domínio e as marcas reconhecíveis (Claro, saúde, fintech), que é prova social barata; (3) **a prova de impacto mais forte que ele tem**, com o "antes" explícito; (4) o diferencial de senioridade (decisões arquiteturais, padrões adotados pelo time).
- **Tempo de experiência abre, mas não sustenta.** `mais de 4 anos dedicados a Flutter` passa no filtro e não convence ninguém sozinho — é o dado mais fraco do bloco. Nenhuma Apresentação deve terminar sem um número de impacto ou um alcance sobre o time.
- **A Apresentação não promete o que as Experiências não provam.** Todo claim ali tem que ter lastro num bloco abaixo. É índice, não vitrine — e é o primeiro lugar onde o recrutador testa a coerência do documento.
- **É onde o auto-elogio mais tenta entrar.** Nenhum `profissional apaixonado`, `visão sistêmica`, `perfil analítico`. Vale a regra geral, com atenção redobrada.

### Estrutura e hierarquia dos blocos de experiência

Todo bloco abre com `\job{empresa}{cargo}{vínculo}{período}{url}` e traz os mesmos campos, nesta ordem: **Descrição da Empresa** (uma linha, o que ela faz), **Projeto** (o produto e o que ele resolve), **Responsabilidades Técnicas**. Projetos pessoais acrescentam **Demo** e **Código**. Não invente campo novo nem troque a ordem: a repetição é o que deixa o documento varrível — o recrutador aprende onde olhar no primeiro bloco e reusa nos outros.

**O formato das Responsabilidades varia de propósito, e é aí que mora a hierarquia visual.** Bullets rotulados por tema (`\lbl{}` dentro de `tight`) onde há peso a distribuir; parágrafo corrido no resto.

Peso se mede por três eixos, e basta um forte:

1. **Recência** — o que ele faz hoje prevê melhor o que vai entregar.
2. **Autoria** — quanto da decisão foi dele (ver camada 1).
3. **Reconhecimento de marca** — se o nome da empresa é a âncora que faz o recrutador parar a varredura, o que está embaixo precisa ser escaneável. Uma marca forte em parágrafo denso desperdiça a atenção que ela mesma conquistou.

Por que a variação em vez de bullets em tudo: a triagem é varredura, não leitura. Bullet oferece uma borda a cada duas linhas onde o olho entra e sai; parágrafo é um bloco em que se entra pelo começo ou não se entra. Se todo item tem marcador, nenhum tem destaque, e a tarefa de descobrir o que importa volta para o recrutador. Parágrafo também é tipograficamente mais barato — os blocos em prosa financiam, dentro das 2 páginas, os bullets dos blocos que importam.

### Nunca

- **Reivindicar cargo ou função que não existiu:** `liderei o time`, `tech lead`, `mentorei`, `gerenciei`. É verificável e destrói o documento inteiro.
- **Declarar lacuna que ninguém perguntou** (`sem experiência em liderança formal`, `conhecimento básico em X`). Currículo não confessa; a entrevista é o lugar de calibrar.
- **Confundir protagonismo com inflar autoria.** Se o teto não permite `conduzi`, o caminho é achar o que **realmente** foi dele naquele projeto e destacar isso, nunca esticar o verbo.

### Métricas — antes/depois de impacto

**Número solto não prova valor. O que prova é o delta, e o delta tem que ser dele.** Classifique todo número antes de escrevê-lo:

| Tipo | Exemplo | Vale? |
|---|---|---|
| **Impacto** — tem estado anterior e posterior, e o delta é dele | `sem nenhum teste → 6.800 testes e 85% de cobertura` | **Sim.** É a única forma que gera valor. Priorize sempre. |
| **Limiar de qualidade** — patamar sustentado, com o mecanismo que o garante | `CI barrando merge abaixo de 80%` | Sim. É o substituto quando não há "antes". |
| **Escala** — dimensiona o ambiente, não a contribuição | `1M+ downloads`, `31 módulos de negócio` | Com moderação, como contexto. Nunca no lugar de impacto. |
| **Contagem bruta** — soma sem referencial | `19 migrations`, `2.3K arquivos Dart` | **Não.** Corte. |

**Decisão do Leandro (Agosto/2026): contagem de testes e percentual de cobertura não entram no currículo.** Nem `6.800 testes / 85%` na Clyvo, nem `968 testes / 90%` no Lions Pontos. A formulação em uso é `alta cobertura de testes automatizados`, com o efeito na frente. Os exemplos com esses números permanecem nesta seção porque ensinam bem o formato antes/depois — mas são material didático, **não texto a reintroduzir no `.tex`**. Não sugira devolvê-los: a decisão já foi tomada e revisitada.

### O número técnico é lastro, não argumento

**O que convence é o valor entregue ao usuário e à empresa. O número técnico entra depois, para provar que aquilo aconteceu.** Cobertura, quantidade de testes e número de módulos medem o *trabalho feito*; menos bug chegando ao usuário, release sem medo, time entregando mais rápido medem o *efeito do trabalho*. O recrutador não compra teste — compra estabilidade, previsibilidade e velocidade. `6.800 testes` sozinho é um número que ele não sabe interpretar; `o time passou a subir versão com segurança` ele entende na hora.

**A ordem dentro da frase importa:** efeito primeiro, número depois como sustentação.

> ❌ `6.800 testes e 85% de cobertura, o que reduziu bugs em produção`
> ✅ `a queda de bugs e regressões deu ao time segurança para subir versão, sustentada por 6.800 testes e 85% de cobertura`

- **Nenhum bloco deve terminar em número técnico.** Se terminar, falta a frase que diz o que aquilo mudou para quem usa o produto ou para quem paga a conta.
- **Efeito sem magnitude é afirmável; magnitude inventada não.** `a queda de bugs e regressões` é relato de algo que ele viveu e defende em entrevista. `bugs caíram 40%` sem fonte viola a camada 1. Direção pode; número inventado não.
- **Traduza toda métrica técnica para o lado de quem recebe.** Cobertura → menos regressão chegando ao usuário. Monorepo → menos atrito entre times, entrega mais rápida. Multi-tenant com RLS → dado de um cliente não vaza para outro. Design system em package → consistência de interface e menos retrabalho.
- **Pergunte ao Leandro antes de assumir que não há efeito para citar.** Ele raramente anotou, mas lembra: se bug parou de voltar, se o time passou a lançar com mais frequência, se a liderança ganhou confiança para demonstrar o produto. Pergunte antes de recuar para a métrica de processo.

Como escrever o antes/depois:

- **O "antes" precisa estar explícito e inequívoco.** `estruturei do zero a estratégia de testes, levando a base a 6.800 testes` é fraco: "do zero" qualifica a estratégia, e o leitor não fica sabendo que a base tinha zero. `entrei num projeto sem nenhum teste automatizado e levei a base a 6.800 testes e 85% de cobertura` mostra o delta. **O "antes" é a metade que carrega o valor — nunca é o que se corta para caber na página.**
- **Prefira a preposição de trajetória** (`de X para Y`, `X → Y`) a números justapostos.
- **Onde houver, feche em consequência de negócio**, não só em número técnico.
- **Sem "antes" documentado, não invente um.** Estimativa arredondada (`reduzi crashes em ~40%`) que ele não consegue defender em follow-up viola a camada 1. Use limiar de qualidade ou escopo, que são verificáveis.
- **Um número forte vale mais que três fracos.** Se contagem bruta e antes/depois competem por espaço, corte a contagem bruta.

## 3. Estilo — o registro da frase

Seco e descritivo. O texto não pode parecer gerado por IA — currículo que soa gerado perde credibilidade antes de ser lido.

- Sem travessão (—) dentro de frase; usar dois-pontos ou vírgula. Travessão como separador estrutural (`MBA ... — ICMC/USP`, `Português — nativo`) pode ficar.
- Sem rótulo em negrito solto no meio do parágrafo; enfiar no fluxo da frase.
- Sem frase de efeito comercial ("leva a consulta completa para o celular").
- Não repetir o mesmo número em duas seções: `31 módulos` fica só nas Responsabilidades Técnicas, onde dimensiona o trabalho dele. **Única exceção: o número-âncora da Apresentação.** Ele reaparece embaixo porque lá faz outro trabalho — no topo é manchete, na experiência é como se chegou até ele. Se o segundo aparecimento não acrescenta nada além do número, é repetição e sai.
- Ao reescrever qualquer bloco, compare o resultado com o texto que ele já tinha escrito e mantenha o mesmo registro.

---

## Git

Commits em português, sem trailer de coautoria. Não commite sem o Leandro pedir. Use `git mv` / `git rm` para arquivos **versionados** (confira com `git ls-files`); auxiliares de build não são versionados, ali `git rm` falha e `rm` é o certo.
