<div align="center">

# LEANDRO ROCHA DE BRITO

### Desenvolvedor Mobile Flutter Sênior

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

Desenvolvedor com 6 anos de experiência, **mais de 4 dedicados a Flutter**, construindo aplicativos para e-commerce, saúde e fintech, incluindo projetos para a **Claro**, com **apps de mais de 1 milhão de downloads**. No último projeto assumi um **MVP sem nenhum teste automatizado** e defini a estratégia de testes do time: o produto **passou do piloto com clientes ao pré-lançamento**. Trabalho com **Clean Architecture**, **conduzi a migração do projeto para monorepo** e **defino os padrões de qualidade adotados pelo time**.

---

## Habilidades

- **Flutter e Dart:** **BLoC** | **Riverpod** | **ValueNotifier** | **ChangeNotifier** | Provider | Get It | Dio | DartZ | Hive | Flutter Secure Storage | fl_chart | Google Maps | Flutter Web (PWA) | Design System próprio | Freezed | GoRouter | build_runner
- **Recursos nativos:** **integração de SDKs e plugins nativos** escritos em Kotlin/Swift em apps Flutter para **Android** e **iOS** | **Biometria facial e OCR de documentos (FaceTec)**
- **Arquitetura:** **Clean Architecture** | MVVM | MVC | **Monorepo (Dart Workspace)** | **modularização em packages** | microapps | MultiRepo | modelagem multi-tenant
- **IA no desenvolvimento:** **Claude Code** como apoio ao desenvolvimento, com **regras de projeto versionadas** para manter a aderência ao padrão do time e **validação em code review**
- **Qualidade e observabilidade:** **Testes unitários e de widget (Mocktail)** | **TDD** | **monitoramento e investigação de incidentes em produção** (**Firebase Crashlytics**, **Sentry**) | **análise de comportamento e produto** (**PostHog**, Microsoft Clarity) | **CI/CD (GitHub Actions, Codemagic)** | **Git Flow** e **trunk-based** | code review
- **Firebase:** Analytics | Firestore | Storage | Remote Config | Cloud Messaging (FCM)
- **Backend e dados:** API REST | **Supabase / PostgreSQL** (Row Level Security, migrations versionadas) | SQLite | MySQL | Docker | gRPC | Cloudflare Workers
- **Distribuição e localização:** publicação, monitoramento e manutenção de apps **em produção** na **Google Play** e **App Store** | push notifications (FCM e OneSignal) | Internacionalização (i18n) e localização (l10n)
- **Outras:** **Git** | GitHub | GitLab | **Scrum** | Kanban | squads multifuncionais | Jira | Figma | VueJS | Astro | Golang

---

## Experiências

### [Clyvo](https://clyvo.global/) — Desenvolvedor Flutter

<sub>PJ &nbsp;·&nbsp; Abril/2026 até Julho/2026 &nbsp;·&nbsp; <a href="https://clyvo.global/">clyvo.global</a></sub>

**Descrição da Empresa:** Startup healthtech brasileira de telemedicina.

**Projeto:** Aplicativo de telemedicina usado pelo médico: cadastro do paciente, agendamento e consulta por videochamada, com sala de espera virtual, à qual o paciente entra por link no WhatsApp. Um **assistente de IA por voz ou texto** apoia a anamnese, com o **diagnóstico final sempre do médico**, e o app emite receita, atestado e encaminhamento **assinados digitalmente**.

**Responsabilidades Técnicas:** **O MVP tinha cinco telas, em multirepo, sem nenhum teste automatizado e sem code review.**

- **Qualidade e testes:** defini a estratégia e os padrões de teste adotados pelo time, levando a base a **alta cobertura de testes automatizados** (unitários e de widget em Mocktail). **Bugs e regressões pararam de voltar**, o time **reduziu retrabalho** e a empresa ganhou confiança para **levar o produto ao piloto com clientes e ao pré-lançamento**. **Introduzi a prática de code review** no time mobile, atuando como revisor. Investiguei os incidentes reportados durante o piloto. **POC de testes E2E com Patrol** e comparativo com Appium para o QA.
- **Arquitetura:** **conduzi a migração de multirepo para monorepo** em Dart Workspace, organizando os **31 módulos de negócio** em packages e refatorando as telas existentes para a Clean Architecture do projeto: o que antes exigia publicar vários repositórios passou a **sair em um PR** e acabaram as **quebras por descompasso de versão**. **Riverpod** no app e **BLoC** no SDK do assistente de IA; **design system e SDK isolados em packages** compartilhados entre os apps.
- **Teleconsulta e onboarding:** **mantive e evoluí** o módulo de videochamada; **integrei a biometria facial e o OCR de documentos** (FaceTec, SDK nativo em Kotlin/Swift) no cadastro do médico, com tratamento de falha e cancelamento de captura; **tratei erro e reautenticação** no fluxo de **assinatura digital**.

---

### [Monetizze](https://www.monetizze.com.br/) — Desenvolvedor Flutter

<sub>PJ &nbsp;·&nbsp; Janeiro/2025 até Março/2026 &nbsp;·&nbsp; <a href="https://www.monetizze.com.br/">monetizze.com.br</a></sub>

**Descrição da Empresa:** Plataforma de vendas online para produtores e afiliados de produtos digitais e físicos.

**Projeto:** Aplicativo mobile para afiliados e produtores digitais, com gestão de vendas, comissões e saques, relatórios, métricas de desempenho e notificações em tempo real. **1M+ downloads** · nota 4,8/5 na Google Play.

**Responsabilidades Técnicas:** **Evoluí** o app em Flutter com **Clean Architecture e BLoC**, integrando APIs REST, Firebase (Crashlytics, Analytics, Remote Config), SQLite e Secure Storage, autenticação biométrica, push via OneSignal e FCM, i18n e gráficos interativos, com testes unitários e code review. Build e publicação em **Codemagic** com GitLab.

---

### [SOFTO](https://sof.to/) — Desenvolvedor Flutter

<sub>PJ &nbsp;·&nbsp; Outubro/2023 até Novembro/2024 &nbsp;·&nbsp; <a href="https://sof.to/">sof.to</a> · <a href="https://www.thefaapp.org">thefaapp.org</a></sub>

**Descrição da Empresa:** Empresa de tecnologia com sedes no Brasil e nos EUA, com clientes como OMS, FGV e Stone.

**Projeto [FA app](https://www.thefaapp.org):** Aplicativo global que conecta médicos, cientistas e famílias na luta contra a Ataxia de Friedreich, doença neurodegenerativa rara, **traduzido para 8 idiomas**. **10K+ downloads** · nota 4,6/5.

**Responsabilidades Técnicas:** **Refatorei a camada visual de 100% das telas** do app, em Flutter com **MVVM e gerência de estado em ChangeNotifier**, melhorando **usabilidade e acessibilidade** e mantendo o layout íntegro nos **8 idiomas**.

---

### [Amaris Consulting](https://amaris.com/) — Desenvolvedor Flutter

<sub>PJ &nbsp;·&nbsp; Abril/2022 até Agosto/2023 &nbsp;·&nbsp; <a href="https://amaris.com/">amaris.com</a> · <a href="https://claropay.com.br/">claropay.com.br</a></sub>

**Descrição da Empresa:** Projeto para a [Claro Pay](https://claropay.com.br/), fintech do grupo Claro focada em serviços financeiros digitais.

**Projeto seguros e assistências técnicas:** **Desenvolvi end-to-end** o módulo de seguros e assistências técnicas, com funcionalidades de contratação, comparação de produtos, gestão de contratos ativos (cancelamento e alteração) e suporte ao cliente. **1M+ downloads** na Google Play.

**Responsabilidades Técnicas:**

- **Arquitetura:** implementei o módulo dentro da **arquitetura de microapps** do projeto, com **monorepo e módulos isolados em packages**, Clean Architecture, gerência de estado em **ValueNotifier** e integração com Firebase e APIs REST.
- **Qualidade:** como erro em contratação ou cancelamento de seguro gera prejuízo financeiro e disputa com o cliente, adotei **TDD** desde o início do módulo, com testes unitários e de widget cobrindo esses fluxos.

---

### [EULABS](https://eulabs.com.br/) — Desenvolvedor Full Stack

<sub>CLT &nbsp;·&nbsp; Dezembro/2020 até Março/2022 &nbsp;·&nbsp; <a href="https://eulabs.com.br/">eulabs.com.br</a></sub>

**Descrição da Empresa:** Software house que desenvolve produtos digitais sob demanda.

**Projeto e-commerce de passagens:** Loja online de venda de passagens rodoviárias, com gestão de vendas e atendimento ao cliente.

**Responsabilidades Técnicas:** **Mantive e evoluí** o e-commerce nas duas pontas: **VueJS** na loja e **Golang** com **MySQL** nos serviços. Na migração do monolito para **microsserviços**, implementei serviços em **gRPC** e **Docker**, deixando cada um subir sem depender do deploy do sistema inteiro.

---

## Projetos Pessoais e Voluntariado

### [Lions Pontos](https://lions-pontos.tektonsoftwares.workers.dev) — Lions Club de Ji-Paraná Centro

<sub>Voluntário &nbsp;·&nbsp; Julho/2026 até o momento</sub>

**Descrição da Empresa:** Clube de serviço do Lions Clubs International, associação sem fins lucrativos; desenvolvo e opero a plataforma como voluntário, sem remuneração.

**Projeto:** Plataforma multi-clube que apura em tempo real o prêmio de associado mais atuante de clubes de serviço, substituindo a apuração manual em atas de papel por um ranking público e auditável. Lançamento de presença pelo celular, extrato individual por associado, tabela de pontos configurável por clube e exportação do ano leonístico. Em piloto no Lions Clube de Ji-Paraná/RO.

**Demo:** [https://lions-pontos.tektonsoftwares.workers.dev/demo](https://lions-pontos.tektonsoftwares.workers.dev/demo)<br>
**Código:** [https://github.com/leandrorochaadm/lions-club-points](https://github.com/leandrorochaadm/lions-club-points)

**Responsabilidades Técnicas:** **Único responsável por todas as decisões técnicas do produto: do modelo de dados ao deploy.**

- **Frontend:** concebi e desenvolvi end-to-end em **Flutter Web** (PWA instalável) com Clean Architecture e Riverpod.
- **Backend e dados:** **Supabase/Postgres** com modelagem **multi-tenant**; como cada clube só pode ver os próprios dados, o isolamento é garantido por **Row Level Security no banco** e não na aplicação. Deploy em **Cloudflare Workers**.
- **Qualidade e operação:** o ranking define um prêmio e erro de cálculo não é aceitável, então sustento **alta cobertura de testes automatizados** com **CI barrando merge** que a reduza. Como não há QA nem suporte, acompanho erro em produção no **Sentry** e uso real no **PostHog**. Os clubes confiam no ranking o bastante para **abandonar a apuração em papel**.
