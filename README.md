<div align="center">

# LEANDRO ROCHA DE BRITO

### Desenvolvedor Mobile Flutter Pleno/Sênior

<sub>
  <a href="https://www.linkedin.com/in/leandrorochaadm">linkedin.com/in/leandrorochaadm</a> &nbsp;·&nbsp;
  <a href="https://github.com/leandrorochaadm">github.com/leandrorochaadm</a> &nbsp;·&nbsp;
  <a href="https://wa.me/5511997118447">(11) 99711-8447</a>
  <br>
  <a href="mailto:leandrorochaadm@gmail.com">leandrorochaadm@gmail.com</a> &nbsp;·&nbsp;
  100% remoto &nbsp;·&nbsp;
  <b>Aberto a propostas</b>
  <br><br>
  <a href="curriculo-leandro-rocha-flutter.pdf"><b>📄 Baixar currículo em PDF</b></a>
</sub>

</div>

---

## Apresentação

Sou desenvolvedor **mobile Flutter** há **mais de 6 anos**, e o que me motiva é ver o time entregar melhor e mais rápido. Passei por fintech, vendas digitais e saúde, no **desenvolvimento de aplicativos Android e iOS** como **Claro Pay** e **Monetizze**, os dois com **mais de 1 milhão de downloads**. Gosto de acompanhar a entrega inteira, em trabalho em equipe com squads multifuncionais. Começo nas cerimônias ágeis, conferindo se a tarefa atende aos requisitos de negócio, passo pelo projeto dos módulos de produto e pelos testes unitários, de integração e de liberação, e termino na construção e publicação dos apps nas lojas. No caminho, mantenho o ambiente de desenvolvimento em ordem, reviso o código gerado por IA com o mesmo critério do resto e, com o app no ar, cuido da resolução de problemas em produção com Crashlytics e Sentry.

Na Clyvo, startup de telemedicina, entrei com o app nas primeiras telas e **cresci com ele até o piloto com médicos reais testando no dia a dia**. Defini a **estratégia de testes automatizados** que o time adotou, e **bugs e regressões pararam de voltar**. Depois migrei o app para monorepo e levei a **revisão de código** (code review) para o time: **as entregas aceleraram** e o pessoal passou a seguir os padrões sem depender de mim.

---

## Habilidades

- **Flutter e Dart:** gerenciamento de estado com **BLoC/Cubit**, **Riverpod**, **ValueNotifier**, **ChangeNotifier** e Provider | **injeção de dependência** (Get It) | Dio | DartZ | Hive | Flutter Secure Storage | fl_chart | Google Maps | Flutter Web (PWA) | Design System próprio com **design tokens** | Freezed | **GoRouter** (rotas aninhadas e shell routes) | build_runner
- **Recursos nativos:** **integração de SDKs e plugins nativos** em Kotlin/Swift para **Android** e **iOS** | **Biometria facial e OCR de documentos (FaceTec)** | **segurança mobile** (armazenamento seguro, autenticação biométrica, reautenticação)
- **Arquitetura de software:** **Clean Architecture** | **SOLID**, **Clean Code**, padrões de projeto e boas práticas de desenvolvimento | arquitetura de aplicativos móveis | MVVM | MVC | **Monorepo (Dart Workspace)** | **modularização de apps em packages** | **microapps (microfrontends)** | MultiRepo | modelagem multi-tenant
- **IA no desenvolvimento:** **Claude Code** com **agentes de IA** executando planos, skills próprias e MCP | levantamento de requisitos, descrição das tarefas no Jira e modelagem das regras de negócio do domínio (**DDD**) | **regras versionadas** adotadas pelo time: código no padrão e mais rápido | **hooks** pre-commit/pre-push: só entra com testes e **revisão**
- **Qualidade e observabilidade:** **Testes unitários e de widget (flutter_test, Mocktail, bloc_test)** | **testes de integração** | **TDD** | **monitoramento e resolução de problemas em produção** (**Firebase Crashlytics**, **Sentry**) | **análise de comportamento e produto** (**PostHog**, Microsoft Clarity) | **CI/CD (GitHub Actions, Codemagic)** | **Git Flow** e **trunk-based**
- **Firebase:** Authentication | Analytics | Firestore | Storage | Remote Config | Cloud Messaging (FCM)
- **Backend e dados:** integração com APIs REST com autenticação JWT | **Supabase / PostgreSQL** (Row Level Security, migrations versionadas) | **PocketBase** (API Rules) | SQLite | Cloudflare Workers (JavaScript/TypeScript)
- **Distribuição e localização:** **desenvolvimento de aplicativos móveis**, publicação em lojas de aplicativos, monitoramento e manutenção de apps **em produção** na **Google Play** e **App Store** (Xcode) | push notifications (FCM e OneSignal) | flavors por ambiente | Internacionalização (i18n) e localização (l10n)
- **Outras:** **Git** (controle de versão) | GitHub | GitLab | **Metodologias ágeis** (**Scrum**, Kanban) | Jira | Figma | Astro

---

## Experiências

### [Clyvo](https://clyvo.global/) — Desenvolvedor Flutter

<sub>PJ &nbsp;·&nbsp; Outubro/2025 até Agosto/2026 &nbsp;·&nbsp; <a href="https://clyvo.global/">clyvo.global</a></sub>

**Descrição da Empresa:** Startup healthtech brasileira de telemedicina.

**Projeto:** Aplicativo de telemedicina usado pelo médico: cadastro do paciente, agendamento e consulta por videochamada e sala de espera virtual. Um **assistente de IA por voz ou texto** apoia a anamnese, com o **diagnóstico final sempre do médico**, e o app emite receita, atestado e encaminhamento **assinados digitalmente**.

**Responsabilidades Técnicas:** **Entrei com o app nas primeiras telas**, em multirepo, e **preparei a base para o piloto**.

- **Qualidade e testes:** defini a estratégia e os padrões de teste adotados pelo time, levando a base a **alta cobertura de testes automatizados** (unitários e de widget em Mocktail). **Bugs e regressões pararam de voltar**, o time **reduziu retrabalho** e a empresa ganhou confiança para **levar o produto ao piloto e ao pré-lançamento**.
- **Code review e produção:** **introduzi a prática de code review** no time mobile, atuando como revisor: **menos bugs chegaram à produção** e o time passou a seguir os padrões sem depender de mim. Investiguei os incidentes do piloto.
- **Arquitetura:** **conduzi a migração de multirepo para monorepo** em Dart Workspace e **estruturei o crescimento do app de cinco telas para 31 módulos de negócio** em packages, refatorando as telas para Clean Architecture por módulo (data, domain, presentation). O que antes exigia publicar vários repositórios passou a **sair em um PR**, as entregas ficaram mais rápidas e acabaram as **quebras por descompasso de versão**. **Riverpod** no app e **BLoC** no SDK do assistente de IA, que **mantive e evoluí**; **ampliei o design system** e o isolei, com o SDK, em packages compartilhados entre os apps.
- **Teleconsulta e onboarding:** **mantive e evoluí** o módulo de videochamada; **integrei a biometria facial e o OCR de documentos** (FaceTec, SDK nativo em Kotlin/Swift) no cadastro do médico, com tratamento de falha e cancelamento de captura; **tratei erro e reautenticação** no fluxo de **assinatura digital**.

---

### [Monetizze](https://www.monetizze.com.br/) — Desenvolvedor Flutter

<sub>PJ &nbsp;·&nbsp; Novembro/2023 até Setembro/2025 &nbsp;·&nbsp; <a href="https://www.monetizze.com.br/">monetizze.com.br</a></sub>

**Descrição da Empresa:** Plataforma de vendas online para produtores e afiliados de produtos digitais e físicos.

**Projeto:** Aplicativo mobile para afiliados e produtores digitais, com gestão de vendas, comissões e saques, relatórios, métricas de desempenho e notificações em tempo real. **1M+ downloads** · nota 4,8/5 na Google Play.

**Responsabilidades Técnicas:** **Evoluí** o app com **Clean Architecture, BLoC e testes unitários**, publicado via **Codemagic**.

- **Operação internacional:** **desenvolvi a vitrine de produtos internacionais**, com comissão por moeda e liberação controlada por Remote Config, e o **cadastro de conta bancária internacional**, com validação de IBAN/SWIFT, para o afiliado promover produtos de fora e sacar em outra moeda.
- **Saque:** como o app movimenta comissões e saques, **desenvolvi o cancelamento de saque** e o filtro por moeda, e mantive a autenticação biométrica e o armazenamento seguro de credenciais.
- **Tratamento de erro:** **migrei os datasources para o novo cliente de API** e **centralizei o tratamento de erro** (sem internet, timeout, sessão expirada, usuário descredenciado), com stack trace no Crashlytics para acompanhar o crash-free rate.
- **Padrões do time:** **criei as regras de lint do projeto**, refatorei os testes de quase todas as features e **escrevi a documentação de onboarding**, padronizando o código e a entrada de novos devs no projeto.

---

### [SOFTO](https://sof.to/) — Desenvolvedor Flutter

<sub>PJ &nbsp;·&nbsp; Janeiro/2022 até Outubro/2023 &nbsp;·&nbsp; <a href="https://sof.to/">sof.to</a> · <a href="https://www.thefaapp.org">thefaapp.org</a></sub>

**Descrição da Empresa:** Empresa de tecnologia com sedes no Brasil e nos EUA, com clientes como OMS, FGV e Stone.

**Projeto [FA app](https://www.thefaapp.org):** Aplicativo global que conecta médicos, cientistas e famílias na luta contra a Ataxia de Friedreich, doença neurodegenerativa rara, **traduzido para 8 idiomas**. **10K+ downloads** · nota 4,6/5.

**Responsabilidades Técnicas:** **Refatorei a camada visual de 100% das telas** do app, em Flutter com **MVVM, gerenciamento de estado em ChangeNotifier** e **Firebase Authentication**, com foco na **experiência do usuário**: melhorei **usabilidade e acessibilidade** e mantive o layout íntegro nos **8 idiomas**.

---

### [Amaris Consulting](https://amaris.com/) — Desenvolvedor Flutter

<sub>PJ &nbsp;·&nbsp; Junho/2020 até Dezembro/2021 &nbsp;·&nbsp; <a href="https://claropay.com.br/">claropay.com.br</a></sub>

**Descrição da Empresa:** Projeto para a [Claro Pay](https://claropay.com.br/), fintech do grupo Claro focada em serviços financeiros digitais.

**Projeto seguros e assistências técnicas:** **Desenvolvi end-to-end** o módulo, com contratação, comparação de produtos, gestão de contratos ativos (cancelamento e alteração) e suporte ao cliente. **1M+ downloads** na Google Play.

**Responsabilidades Técnicas:**

- **Arquitetura:** implementei o módulo dentro da **arquitetura de microapps (microfrontends)**, com **monorepo e módulos isolados em packages**, Clean Architecture, estado em **ValueNotifier** e integração com Firebase e APIs REST.
- **Qualidade:** como erro em contratação ou cancelamento de seguro gera prejuízo financeiro e disputa com o cliente, adotei **TDD** desde o início do módulo, com testes unitários e de widget cobrindo esses fluxos.

---

## Projetos Pessoais e Voluntariado

### [Lions Pontos](https://lions-pontos.tektonsoftwares.workers.dev) — Lions Club de Ji-Paraná Centro

<sub>Voluntário &nbsp;·&nbsp; Julho/2026 até o momento</sub>

**Descrição da Empresa:** Clube de serviço do Lions Clubs International; trabalho voluntário, sem remuneração.

**Projeto:** Plataforma multi-clube que apura em tempo real o prêmio de associado mais atuante, com ranking público e auditável. O clube piloto, de Ji-Paraná/RO, trocou as atas de papel pelo ranking, e a expansão prevista é a região norte.

**Demo:** [lions-pontos.tektonsoftwares.workers.dev/demo](https://lions-pontos.tektonsoftwares.workers.dev/demo) &nbsp; **Código:** [github.com/leandrorochaadm/lions-club-points](https://github.com/leandrorochaadm/lions-club-points)

**Responsabilidades Técnicas:** **Único responsável pelas decisões técnicas, do modelo de dados ao deploy.**

- **Frontend:** concebi e desenvolvi o PWA em **Flutter Web**, com Clean Architecture e Riverpod, em **Cloudflare Workers**.
- **Backend e dados:** a regra de negócio estava duplicada em SQL e Dart; para deixá-la só no domain, migrei de Supabase para **PocketBase** numa **VPS própria**, com os dados do piloto. O isolamento **multi-tenant** entre clubes fica nas **API Rules**.
- **Qualidade e operação:** o ranking define um prêmio e erro de cálculo não é aceitável, então sustento **alta cobertura de testes automatizados**, com **CI barrando merge** que a reduza ou quebre o isolamento. Erro no **Sentry**, uso no **PostHog**.
