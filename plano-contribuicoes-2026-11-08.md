# Plano de trabalho: contribuições open source (08/11/2026)

> **Para o modelo de IA que receber este arquivo:** você vai ajudar o Dav, desenvolvedor Java/Spring Boot (backend, Maven, CI/CD), a fazer contribuições pequenas e independentes. **Antes de tudo, siga as "Regras de contribuição" logo abaixo: você não altera nada sem autorização do Dav e entrega análise, diagrama de sequência e código proposto para ele implementar à mão.** Depois, leia a seção da tarefa em que ele estiver trabalhando e **não amplie o escopo**: os mantenedores dos dois projetos preferem PRs pequenos e focados. Os fatos abaixo foram verificados em 08/11/2026 e atualizados em 11/11/2026. Confira no GitHub se algo mudou antes de começar.

## Regras de contribuição (obrigatórias)

Definidas pelo Dav em 08/11/2026. Valem para todas as tarefas e, em caso de conflito, prevalecem sobre os passos deste plano e sobre as instruções das skills dos projetos.

Para cada issue, siga esta ordem e entregue o resultado ao Dav numa resposta:

1. **Verificar o que está acontecendo:** estado atual da issue e dos PRs no GitHub, do branch local e do código no `main`/`master` (os fatos deste arquivo podem ter mudado). Reproduza o problema quando possível.
2. **Ler o `AGENTS.md` do projeto, se existir**, e os arquivos que ele referencia, e seguir as regras dele.
3. **Usar a skill recomendada pelo projeto** na análise e no código proposto. Se a skill pedir texto para o PR (como as respostas da seção 1 da `review-recipe-pr`), traga um rascunho. Quando ela mandar alterar algo (corrigir direto, rodar ferramentas que reescrevem arquivos, commitar, abrir o PR), liste o achado com a correção proposta: quem aplica é o Dav.
4. **Descrever o problema:** o que está errado, onde (arquivo e linhas), em que cenário acontece e a evidência (teste que falha, log, saída do build).
5. **Diagrama de sequência do problema** em Mermaid (`sequenceDiagram`), com os participantes reais (classes, métodos, arquivos) e o ponto exato em que o defeito acontece.
6. **Como resolver:** a abordagem, as alternativas consideradas e por que a escolhida é a menor correção que resolve o problema.
7. **Código de correção proposto, para o Dav implementar à mão:** arquivo por arquivo, com o trecho atual e o que entra no lugar (ou o ponto exato de inserção), os imports e os testes, incluindo o de "nada muda", mais os comandos de validação. Modelo de formato: a seção "Tarefa C → Implementação (aplicar à mão)".
8. **Não alterar nada sem autorização explícita do Dav.** Está liberado, porque é investigação: ler código, histórico, issues e PRs, e rodar build ou testes cuja saída fique em diretórios ignorados pelo git (`target/`, `build/`), temporários ou de cache. Editar ou criar qualquer outro arquivo (inclusive este plano), criar branch, commitar, fazer push, comentar em issue e abrir ou atualizar PR só com autorização do Dav para aquela ação específica. Uma autorização não vale para a próxima ação.
9. **Proibido mencionar IA ou usar estilo artificial em commits, PRs e comentários:**
   - **Zero atribuição de IA:** nunca incluir `Generated with...`, `Co-Authored-By:` de bots/agentes (Devin, Claude, Copilot, Cursor, Gemini, etc.) ou qualquer menção a IA, LLM, agente ou assistente em mensagens de commit, títulos/descrições de PR ou comentários em issues.
   - **Sem travessões típicos de IA (`—` / `--`):** não usar travessões longos (`—`, *em-dash*) ou meia-risca (`–`, *en-dash*) para conectar frases nas mensagens de commit, descrições de PR ou comentários no código/GitHub. Prefira pontuação natural (vírgula, dois-pontos, ponto final ou parênteses).
   - **Escrita humana e no padrão do repositório:** títulos e mensagens de commit e descrições de PR devem ser diretos, concisos, naturais e escritos como um desenvolvedor humano experiente escreve, seguindo o histórico real do repositório (`git log` do `upstream/main`).

**Este arquivo (branch `planos`):**
- Este plano existe **só no fork**: versionado na branch `planos` do `origin` (fork `DavJaveiro/rewrite-spring`) e ignorado localmente via `.git/info/exclude` (padrão `plano-contribuicoes-*.md`) — não aparece no `git status`, em commits nem em PRs.
- **Nunca criar branch de contribuição a partir de `planos`** — sempre a partir de `main` atualizado com `upstream/main`. Branches filhas de `planos` carregam o commit deste arquivo, que vazaria no diff do PR para o upstream.
- Para editar e sincronizar este plano: `git switch planos` → editar → `git commit -am "..." && git push` → `git switch -`. **Atenção:** o switch para `planos` sobrescreve a cópia local ignorada — commitar edições antes; e, ao voltar para `main`, o arquivo some da pasta (é tracked só em `planos`). Para trazê-lo de volta sem sair de `main`: `git restore --source=planos -- plano-contribuicoes-2026-11-08.md`.
- Em outra máquina (uma vez): adicionar `plano-contribuicoes-*.md` ao `.git/info/exclude`, depois `git fetch origin` e `git restore --source=origin/planos -- plano-contribuicoes-2026-11-08.md`.

**Regras de cada projeto** (verificado em 08/11/2026):
- **`rewrite-spring`:** tem `AGENTS.md` na raiz (o `CLAUDE.md` só faz `@AGENTS.md`). Ele pede autorrevisão com a skill `review-recipe-pr` (`.claude/skills/review-recipe-pr/SKILL.md`) antes de abrir o PR, com as respostas da seção 1 ("Is this the right change?") na descrição, e PRs pequenos: um passo de migração de um padrão comum, com testes de antes e depois. A skill compara com `origin/main`, mas neste clone `origin` é o fork (`DavJaveiro/rewrite-spring`) e `upstream` é o `openrewrite/rewrite-spring`: use `upstream/main`.

---

## Visão geral

|          | Tarefa B                                                                                                 | Tarefa C                                                                                                 | Tarefa D                                                                                                    |
| -------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Projeto  | `openrewrite/rewrite-spring`                                                                             | `openrewrite/rewrite-spring`                                                                             | `openrewrite/rewrite-spring`                                                                                |
| Issue    | [#1201 – item **B4**](https://github.com/openrewrite/rewrite-spring/issues/1201)                         | [#1201 – item **B6**](https://github.com/openrewrite/rewrite-spring/issues/1201)                         | [#1201 – item **B3**](https://github.com/openrewrite/rewrite-spring/issues/1201)                            |
| Situação | PR [#1270](https://github.com/openrewrite/rewrite-spring/pull/1270) atualizado e testado (8/8); **ready for review, mas o `cgp` falhou por 503 no plugin `recipe-library`** | PR [#1271](https://github.com/openrewrite/rewrite-spring/pull/1271) atualizado e testado (12/12); **ready for review, `cgp` falhou pelo mesmo 503** | PR [#1283](https://github.com/openrewrite/rewrite-spring/pull/1283) **APROVADO E MERGEADO** em 11/11/2026 (`3231afb3`) |
| Esforço  | M (meio dia a 1 dia)                                                                                     | M (meio dia)                                                                                             | P–M (mesma forma do B4/B6)                                                                                  |
| Build    | Gradle (`./gradlew`)                                                                                     | Gradle (`./gradlew`)                                                                                     | Gradle (`./gradlew`)                                                                                        |

**Status geral (atualizado em 11/11/2026):** A Tarefa D (**B3**, PR #1283) foi revisada, elogiada pelo mantenedor `timtebeek` (*"Thanks a lot! This indeed is the pattern we'd expect."*) e mergeada na `upstream/main` (`3231afb3`). As Tarefas B (**B4**, PR #1270) e C (**B6**, PR #1271) foram alinhadas com o mesmo padrão enxuto aprovado na B3, rebaseadas sobre `upstream/main`, validadas localmente (8/8 e 12/12 testes passando) e enviadas para o `origin`. O `main` local e o do fork foram sincronizados com a `upstream/main` em 11/11/2026 (`3231afb3`; a última tag é `v6.53.0`, em `9fd585b4`). As PRs #1270 e #1271 já estão como ready for review (não são mais draft), mas o check `cgp` falhou em 11/11/2026 às 19:24 UTC: 503 do repositório do CGP ao resolver o plugin `org.openrewrite.build.recipe-library:2.41.0`, e o build parou antes de compilar e rodar os testes, então o vermelho não indica falha dos testes; falta uma nova execução do `cgp` ou validação pelo mantenedor.

---

## Progresso (atualizado em 11/11/2026)

### Tarefa B (B4) — alinhada ao padrão da B3, 8/8 testes passando, enviada na PR #1270

**Implementação** (branch `b4-logging-shutdown-hooks-per-project`, commit `9001d9c7` rebaseado sobre `upstream/main` (`3231afb3`)):
- `ScanningRecipe<AtomicBoolean>` -> `ScanningRecipe<Set<JavaProject>>` (um `JavaProject` por módulo aplicável).
- Scanner: `TreeVisitor` genérico sobre `SourceFile` com curto-circuito `acc.contains(maybeJavaProject.get())`; com `MavenResolutionResult` aplica a regra original (packaging `jar` + dep compile `spring-boot:2.4.X`); com `GradleProject`, exige plugin `war` ausente (`"war".equals(plugin.getId()) || "org.gradle.war".equals(plugin.getId()) || plugin.getFullyQualifiedClassName().startsWith("org.gradle.api.plugins.WarPlugin")`) e dep resolvida `spring-boot:2.4.X` via `gradleProject.getConfiguration("compileClasspath")` e `configuration.findResolvedDependency("org.springframework.boot", "spring-boot")`.
- Visitor: `Preconditions.check` verificando se o `JavaProject` do arquivo está no conjunto acumulado antes de aplicar `FindAnnotations`.

**Testes:** **8/8 passando** (`LoggingShutdownHooksTest`: 5 testes existentes embrulhados em `mavenProject(...)` + 3 novos: `onlyApplicableModulesAreMarked`, `gradleJarProject` e `gradleWarProject` com `withToolingApi`).

**PR:** https://github.com/openrewrite/rewrite-spring/pull/1270

### Tarefa C (B6) — alinhada ao padrão da B3, 12/12 testes passando, enviada na PR #1271

**Implementação** (branch `b6-gradle-support-search-recipes`, commits `bc4c6fce` + `34088071` rebaseados sobre `upstream/main` (`3231afb3`)):
- `FindIntegrationSchedulerPool`: detecção por marcador (`MavenResolutionResult` -> `SPRING_BOOT_24` + `!model.findDependencies("org.springframework.integration", "spring-integration-core", Scope.Compile).isEmpty()`; `GradleProject` -> `gradleProject.getConfiguration("compileClasspath")` + `findResolvedDependency(...)` para `spring-boot` 2.4.X e `spring-integration-core`).
- `spring-boot-25.yml`: `maven.search.FindDependency` -> `org.openrewrite.java.dependencies.FindDependency` (unificada; delega para Maven e Gradle mantendo a semântica).
- **Testes:** **12/12 passando** (`FindIntegrationSchedulerPoolTest` 9/9 + `MessagesInTheDefaultErrorViewTest` 3/3).

**PR:** https://github.com/openrewrite/rewrite-spring/pull/1271

### Tarefa D (B3) — concluída, aprovada e MERGEADA na `upstream/main` (#1283)

**Implementação** (branch `b3-sleuth-logging-pattern-per-project`, commit `6debc48a`, mergeado na `upstream/main` como `3231afb3` em 11/11/2026):
- `AddLoggingPatternLevelForSleuth`: `ScanningRecipe<Set<JavaProject>>` usando `!model.findDependencies("org.springframework.cloud", "spring-cloud-starter-sleuth", Scope.Compile).isEmpty()` para Maven e `gradleProject.getConfiguration("compileClasspath")` + `findResolvedDependency("org.springframework.cloud", "spring-cloud-starter-sleuth")` para Gradle.
- **Testes:** **5/5 passando** (`AddLoggingPatternLevelForSleuthTest`: `addLoggingPatternWhenUsingSleuth` e `doNotAddWhenNotUsingSleuth` existentes + `onlyAddToModuleUsingSleuth`, `gradleProjectUsingSleuth` e `gradleProjectNotUsingSleuth`).
- **PR:** https://github.com/openrewrite/rewrite-spring/pull/1283 (aprovado e mergeado por `timtebeek`).

### Pendências externas
- PRs #1270 (B4) e #1271 (B6): ready for review; o `cgp` falhou por 503 na resolução do plugin `org.openrewrite.build.recipe-library:2.41.0` antes de compilar/testar. Aguardando nova execução do `cgp` (ou validação pelo mantenedor) e revisão/merge.

## Tarefa B: rewrite-spring #1201, item B4 (`LoggingShutdownHooks`)

### Contexto
- A #1201 é um checklist do mantenedor Tim te Beek (`timtebeek`) com dezenas de correções em receitas. O Dav reservou o **B4**. Não pegue outros itens no mesmo PR.
- O que o B4 diz: *"A global flag marks application classes in every module, and detection is Maven-only. Key by project and add Gradle detection."*
- Arquivos (verificados no commit `8d28618`):
  - Receita: `src/main/java/org/openrewrite/java/spring/boot2/search/LoggingShutdownHooks.java`
  - Teste: `src/test/java/org/openrewrite/java/spring/boot2/search/LoggingShutdownHooksTest.java`
  - Uso: `src/main/resources/META-INF/rewrite/spring-boot-25.yml`, na lista de buscas do upgrade para o Boot 2.5.
- **Como a receita funciona hoje:**
  - É uma `ScanningRecipe<AtomicBoolean>`.
  - O scanner é um `MavenVisitor`. Se **algum** `pom.xml` tem packaging `jar` e depende de `org.springframework.boot:spring-boot:2.4.X` (escopo compile), ele liga um **único booleano global**.
  - O visitor aplica `FindAnnotations("@org.springframework.boot.autoconfigure.SpringBootApplication")` em **todos** os arquivos, desde que o booleano esteja ligado.
- **Bugs:**
  1. Num projeto multimódulo, se um módulo atende à condição, o `@SpringBootApplication` de **outro** módulo também é marcado, mesmo sendo `war` ou outra versão do Boot.
  2. Projetos Gradle nunca são detectados.
- **Modelo a seguir, no mesmo pacote:** `FindIntegrationSchedulerPool.java` já guarda estado **por projeto**, usando o marcador `JavaProject` (`org.openrewrite.java.marker.JavaProject`) em `Set`s dentro de um acumulador `JavaProjects`. Para Gradle, veja como `MergeBootstrapYamlWithApplicationYaml.java`, `SpringConfigFiles.java` e `org/openrewrite/gradle/spring/*.java` usam o marcador `GradleProject`.

### Regras do repositório (ler antes)
- `AGENTS.md` na raiz: antes de abrir o PR, faça a autorrevisão com a skill `.claude/skills/review-recipe-pr/SKILL.md` e responda na descrição do PR as perguntas da seção 1 dela ("Is this the right change?").
- O PR deve ser **pequeno, bem testado e simples**. Ter um teste de "nada muda" é obrigatório.
- O commit `8d28618`/#1202 ("Keep values, not trees or visitors, in scanning recipe accumulators") pede que o acumulador guarde **valores** (por exemplo, o `JavaProject` ou o id dele), nunca árvores ou visitors.

### Passos
> Status em 11/11: passos 1 a 6 concluídos (PR #1270 pronta para revisão, 8/8 testes locais). Falta o 7, depois do merge.

1. **Ambiente:**
   ```bash
   # fork no GitHub, depois:
   git clone https://github.com/<usuario>/rewrite-spring.git
   cd rewrite-spring
   git checkout -b b4-logging-shutdown-hooks-per-project
   ./gradlew compileJava
   ```
   - Se der 401/403 ao resolver o plugin `org.openrewrite.build.recipe-library` ou artefatos da Moderne ("Code Genome"), **não insista**. O mantenedor disse na #1201 que validar pelo CI do PR é aceitável. Nesse caso, abra o PR como *draft* e acompanhe o CI.
2. **Escrever os testes primeiro**, em `LoggingShutdownHooksTest`, no estilo `rewriteRun(...)` com `mavenProject(...)` (ou o equivalente usado no repositório) para separar os módulos:
   - **Multimódulo Maven:** o módulo `app-a` é jar com Boot 2.4.x e deve ser marcado; o módulo `app-b` é war (ou Boot 2.5) e **não** deve ser marcado. Hoje esse teste deve falhar.
   - **Gradle:** um `build.gradle` com `org.springframework.boot:spring-boot:2.4.x` e uma classe `@SpringBootApplication`, que deve ser marcada. Use os helpers de teste Gradle que outros testes do repositório já usam (procure `buildGradle(` e `withToolingApi` em `src/test`).
   - **Gradle war:** com o plugin `war` aplicado, a classe não deve ser marcada, para manter a regra de packaging.
   - Os testes existentes (`noExplicitPackagingType`, `explicitJarPackagingType`, `explicitWarPackagingType`, `lowerBootProject`, `higherBootProject`) devem continuar passando.
3. **Implementar:**
   - Trocar o `AtomicBoolean` por um acumulador com `Set<JavaProject>` (ou ids), com os projetos aplicáveis.
   - **Scanner:** para cada `SourceFile`:
     - Se for documento Maven (tem o marcador `MavenResolutionResult`), aplique a regra atual (packaging `jar` e dependência compile `spring-boot:2.4.X`) e, se bater, adicione o `JavaProject` do arquivo ao conjunto.
     - Se tiver o marcador `GradleProject`, aplique a regra equivalente: dependência resolvida em `compileClasspath`/`runtimeClasspath` que bata com `spring-boot:2.4.X`, e plugin `war` ausente. Confira na API do `GradleProject` como ler dependências e plugins; não invente métodos.
   - **Visitor:** só rodar o `FindAnnotations` se o `JavaProject` do arquivo Java estiver no conjunto.
   - Manter `displayName` e `description`.
4. **Validar:**
   ```bash
   ./gradlew test --tests "*LoggingShutdownHooksTest"
   ./gradlew test   # se o ambiente permitir; senão, o CI
   ```
5. **Autorrevisão:** siga a skill `review-recipe-pr` contra `origin/main` e corrija o que ela apontar.
6. **PR:**
   - Título sugerido: `LoggingShutdownHooks: track applicable projects per module and detect Gradle builds (B4 of #1201)`.
   - Descrição: o problema (flag global + só Maven), a solução (estado por `JavaProject` + detecção Gradle), a lista dos testes novos, as respostas à seção 1 da skill e `Part of #1201 (B4)`. Use **"Part of"**, não "Fixes", para não fechar o checklist inteiro.
   - Confira no `CONTRIBUTING`/README se o projeto pede DCO. Se pedir, `git commit -s`.
7. **Depois do merge:** comente na #1201 avisando que o B4 foi resolvido com o link do PR. É o mantenedor quem marca o item como feito.

### Critério de pronto
- Os testes novos de multimódulo e Gradle passam, e os antigos também.
- O acumulador guarda valores, não árvores.
- O diff fica restrito a `LoggingShutdownHooks.java` e `LoggingShutdownHooksTest.java`.

---

## Tarefa C: rewrite-spring #1201, item B6 (detecção Gradle em receitas de busca só-Maven)

### Contexto
- Segundo item da #1201 reservado pelo Dav (o B4 virou o PR #1270). Mesmo protocolo: comentar `I'd like to take B6` na issue.
- O item cita dois pontos:
  1. `IntegrationSchedulerPoolRecipe.java:76-101,167-172` — no repo atual o arquivo é `src/main/java/org/openrewrite/java/spring/boot2/search/FindIntegrationSchedulerPool.java` (renomeado; é a mesma receita citada no A3). O acumulador já é por `JavaProject` — **não** há bug de flag global. O problema é só a detecção: o scanner só adiciona a `applicableProjects` quando encontra `Xml.Document` + `MavenResolutionResult`. Em projetos Gradle nenhum arquivo tem esse marcador → `applicableProjects` fica vazio → `getVisitor` retorna `noop` → nenhum comentário é adicionado.
  2. `spring-boot-25.yml:134-139` — `MessagesInTheDefaultErrorView` (declarativa) usa `org.openrewrite.maven.search.FindDependency` 2× (`spring-webmvc`, `spring-webflux`): o `MavenIsoVisitor` só visita `Xml.Document`, então `build.gradle` nunca é marcado.
- **Escopo:** só a detecção Gradle. O **A3** (wiring de `FindIntegrationSchedulerPool` em `FindUpgradeRequirementsSpringBoot_2_5`) é item da seção A, que exige decisão do mantenedor — **não** incluir no PR.

### Diagnóstico (verificado em 08/11/2026, branch `b4-logging-shutdown-hooks-per-project` = main + B4)
- `FindIntegrationSchedulerPool`: scanner em `:160-165` (`instanceof Xml.Document` → `isApplicableMavenProject`, que exige `spring-boot:2.4.X` + `spring-integration-core` em `Scope.Compile`); visitor em `:196-251` filtra `sourceToCommentByProject` por `applicableProjects`.
- `maven.search.FindDependency` marca apenas `<dependency>` **declaradas** no pom ("first-order", sem transitivas). A unificada `org.openrewrite.java.dependencies.FindDependency` (módulo `rewrite-java-dependencies`, já no classpath — usada em `spring-boot-40-modular-starters.yml`) delega para `maven.search.FindDependency` + `gradle.search.FindDependency` com as mesmas opções: **troca 1:1 que preserva a semântica e adiciona Gradle**.
- Modelo de código: o próprio B4 (`LoggingShutdownHooks`, commit `4d5a842`) — `GradleProject`, `getConfiguration("compileClasspath"|"runtimeClasspath")`, `getResolved()` (cobre transitivas, espelha `Scope.Compile`).
- Em runs reais o marcador `GradleProject` vem em todos os arquivos do projeto; no teste (`withToolingApi`) vem só no `build.gradle`, que ganha `JavaProject` via `mavenProject(...)`. Checar o marcador **por arquivo** (não por tipo de arquivo) cobre os dois mundos.

### Implementação (aplicar à mão)

**1. `FindIntegrationSchedulerPool.java`**

Imports novos (e remover `import org.openrewrite.xml.tree.Xml;`, que fica sem uso):
```java
import org.openrewrite.gradle.marker.GradleDependencyConfiguration;
import org.openrewrite.gradle.marker.GradleProject;
```

Constantes novas (junto dos `Pattern`s no topo da classe):
```java
private static final DependencyMatcher SPRING_BOOT_24 = requireNonNull(
        DependencyMatcher.build("org.springframework.boot:spring-boot:2.4.X").getValue());
private static final DependencyMatcher SPRING_INTEGRATION = requireNonNull(
        DependencyMatcher.build("org.springframework.integration:spring-integration-core").getValue());
private static final List<String> CLASSPATH_CONFIGURATIONS = Arrays.asList("compileClasspath", "runtimeClasspath");
```

Substituir `isApplicableMavenProject` (`:71-94`; muda a assinatura para receber o marcador) e adicionar a irmã Gradle:
```java
private static boolean isApplicableMavenProject(MavenResolutionResult model) {
    boolean boot24 = false;
    boolean springIntegration = false;
    for (ResolvedDependency d : model.getDependencies().getOrDefault(Scope.Compile, emptyList())) {
        if (!boot24) {
            boot24 = SPRING_BOOT_24.matches(d.getGroupId(), d.getArtifactId(), d.getVersion());
        }
        if (!springIntegration) {
            springIntegration = SPRING_INTEGRATION.matches(d.getGroupId(), d.getArtifactId());
        }
        if (boot24 && springIntegration) {
            return true;
        }
    }
    return false;
}

private static boolean isApplicableGradleProject(GradleProject gradleProject) {
    boolean boot24 = false;
    boolean springIntegration = false;
    for (String configurationName : CLASSPATH_CONFIGURATIONS) {
        GradleDependencyConfiguration configuration = gradleProject.getConfiguration(configurationName);
        if (configuration == null) {
            continue;
        }
        for (ResolvedDependency d : configuration.getResolved()) {
            if (!boot24) {
                boot24 = SPRING_BOOT_24.matches(d.getGroupId(), d.getArtifactId(), d.getVersion());
            }
            if (!springIntegration) {
                springIntegration = SPRING_INTEGRATION.matches(d.getGroupId(), d.getArtifactId());
            }
            if (boot24 && springIntegration) {
                return true;
            }
        }
    }
    return false;
}
```

No scanner, substituir o primeiro ramo `if (source instanceof Xml.Document) { ... }` (`:160-165`) por checagem por marcador (o `Xml.Document` deixa de ser testado por tipo — `MavenResolutionResult` só existe em pom.xml mesmo):
```java
if (!acc.getApplicableProjects().contains(javaProject)) {
    Optional<MavenResolutionResult> maven = source.getMarkers().findFirst(MavenResolutionResult.class);
    if (maven.isPresent()) {
        if (isApplicableMavenProject(maven.get())) {
            acc.getApplicableProjects().add(javaProject);
        }
    } else if (source.getMarkers().findFirst(GradleProject.class)
            .map(FindIntegrationSchedulerPool::isApplicableGradleProject).orElse(false)) {
        acc.getApplicableProjects().add(javaProject);
    }
}
```
...e mudar o `else if (source instanceof Properties ...)` seguinte para `if` (ele vira o primeiro ramo da cadeia). O resto da cadeia (`else if` Yaml.Documents, `else if` JavaSourceFile) fica igual. Um `build.gradle` (`G.CompilationUnit`, que é `JavaSourceFile`) cai no último ramo, onde `usesSpringBootApplication` retorna falso sem custo.

**2. `spring-boot-25.yml`** (`:133-138`):
```yaml
recipeList:
  - org.openrewrite.java.dependencies.FindDependency:
      groupId: org.springframework
      artifactId: spring-webmvc
  - org.openrewrite.java.dependencies.FindDependency:
      groupId: org.springframework
      artifactId: spring-webflux
```

### Testes
- `FindIntegrationSchedulerPoolTest`: adicionar imports `static org.openrewrite.gradle.Assertions.buildGradle` e `static org.openrewrite.gradle.toolingapi.Assertions.withToolingApi` e dois testes no molde de `gradleJarProject`/`gradleWarProject` do `LoggingShutdownHooksTest` (`spec.beforeRecipe(withToolingApi())`, `mavenProject("project", srcMainJava(java(...)), buildGradle(...))`):
  - `gradleProject`: `implementation 'org.springframework.boot:spring-boot-starter-integration:2.4.13'` → a classe `@SpringBootApplication` ganha o comentário `// TODO: Scheduler thread pool size...`.
  - `gradleProjectWithoutSpringIntegration`: só `spring-boot-starter:2.4.13` → sem comentário.
- Novo `MessagesInTheDefaultErrorViewTest` com `spec.recipeFromResources("org.openrewrite.java.spring.boot2.search.MessagesInTheDefaultErrorView")`: `spring-webmvc` declarada no pom sai com `<!--~~>--><dependency>`; `spring-webflux` no `buildGradle` sai com `/*~~>*/implementation '…'`; e um teste sem correspondência. `buildGradle` não precisa de `withToolingApi` (o `GradleDependency` trait casa declarações sintaticamente).
- Os testes Maven existentes devem continuar verdes (detecção Maven inalterada).

### Passos
> Status em 11/11: passos 1 a 6 concluídos (comentário na #1201 e PR #1271 pronta para revisão, 12/12 testes locais). Falta o 7, depois do merge.

1. `git checkout main && git pull upstream main && git checkout -b b6-gradle-support-search-recipes` — **branch novo a partir de `main`**, não do branch do B4 (arquivos não se sobrepõem; manter PRs independentes).
2. Comentar na #1201: `I'd like to take B6` (protocolo do checklist).
3. Aplicar o código à mão (seções acima), testes primeiro.
4. Validar como no B4: `./gradlew` não resolve o plugin `recipe-library` (credenciais Code Genome) — compilar com `javac` + jars `rewrite-*` do Maven Central e abrir PR **draft** para o CI validar. Ou `./gradlew test --tests "*FindIntegrationSchedulerPoolTest" --tests "*MessagesInTheDefaultErrorViewTest"` se o ambiente resolver.
5. Autorrevisão com a skill `review-recipe-pr` contra `origin/main`.
6. PR — título: `Add Gradle detection to FindIntegrationSchedulerPool and MessagesInTheDefaultErrorView (B6 of #1201)`; descrição com `Part of #1201 (B6)` (não "Fixes") + respostas da seção 1 da skill.
7. Após merge: comentar na #1201 com o link do PR (o mantenedor marca o item).

### Critério de pronto
- Testes Gradle novos passam + testes Maven antigos verdes.
- Diff restrito a `FindIntegrationSchedulerPool.java`, `FindIntegrationSchedulerPoolTest.java`, `spring-boot-25.yml` e o novo `MessagesInTheDefaultErrorViewTest.java`.
- `MessagesInTheDefaultErrorView` marca dependências declaradas em pom.xml **e** build.gradle.

---

## Tarefa D: rewrite-spring #1201, item B3 (`AddLoggingPatternLevelForSleuth`)

### Contexto
- Terceiro item da #1201 escolhido pelo Dav (B4 = PR #1270, B6 = PR #1271). O Dav comentou `I'd like to take B3` na issue em 10/11/2026 e a correção foi mergeada em 11/11/2026 via PR #1283. O B3 diz: *"per-project state and Gradle support"*, mesmo formato de defeito do B4.
- Arquivos (verificados em 08/11/2026, sobre a `main` de então):
  - Receita: `src/main/java/org/openrewrite/java/spring/cloud2022/AddLoggingPatternLevelForSleuth.java`
  - Teste: `src/test/java/org/openrewrite/java/spring/cloud2022/AddLoggingPatternLevelForSleuthTest.java`
  - Uso: `src/main/resources/META-INF/rewrite/spring-cloud-2022.yml:98`.
- **Como a receita funcionava antes da correção** (`:35-71`, na `main` de 08/11):
  - `ScanningRecipe<AtomicBoolean>` — um booleano **global** (`:35,:44-45`).
  - O scanner é um `MavenVisitor` (`:49`): em qualquer `pom.xml` com `org.springframework.cloud:spring-cloud-starter-sleuth:X` em `Scope.Compile`, liga a flag (`:52-55`).
  - O visitor roda `Preconditions.check(acc.get(), new AddSpringProperty("logging.pattern.level", "%5p [${spring.application.name:},%X{traceId:-},%X{spanId:-}]", "...comment...", null).getVisitor())` (`:63-69`) — injeta a propriedade em `application.properties`/`application.yml`.
- **Bugs:**
  1. Num projeto multimódulo, **um** módulo com Sleuth liga a flag global → `logging.pattern.level` é adicionado nas configs de **todos** os módulos (inclusive `src/test/resources`).
  2. Projetos Gradle nunca são detectados (`MavenVisitor` só visita `Xml.Document`).

### Diagnóstico (verificado em 08/11/2026)
- A diferença conceitual em relação ao B4/B6: o alvo aqui **não é** uma classe Java nem um marcador `SearchResult` — é o arquivo de config (`application.*`). O gate por projeto precisa checar o `JavaProject` **do próprio arquivo de config**, dentro do `Preconditions.check` (mesmo truque do B4: o check retorna `SearchResult.found` quando o `JavaProject` do arquivo ∈ set; o marcador do check é descartado).
- Regra Maven original: `DependencyMatcher.build("org.springframework.cloud:spring-cloud-starter-sleuth:X")` em `Scope.Compile` (`:53-55`) — **sem** checagem de packaging (não copiar a regra `war` do B4; aqui é como o B6).
- Regra Gradle espelhada: `GradleProject` → `getConfiguration("compileClasspath"|"runtimeClasspath")` → `getResolved()` (cobre transitivas, espelha `Scope.Compile`) com o mesmo matcher.
- Nos testes atuais (`AddLoggingPatternLevelForSleuthTest`), os casos já vêm embrulhados em `mavenProject("project", pomXml(...), properties(...), yaml(...))` — o wrapper fornece o marcador `JavaProject` aos arquivos filhos, então os testes Maven existentes devem continuar verdes sem alteração.

### Implementação (como ficou, mergeada em `3231afb3`)
- `ScanningRecipe<AtomicBoolean>` virou `ScanningRecipe<Set<JavaProject>>` com `HashSet`, guardando valores e não árvores (conforme #1202).
- **Scanner:** `TreeVisitor<Tree, ExecutionContext>` que só considera `SourceFile`; lê o marcador `JavaProject` e faz curto-circuito quando o projeto já está no conjunto.
  - Com `MavenResolutionResult`, usa `findDependencies("org.springframework.cloud", "spring-cloud-starter-sleuth", Scope.Compile)`.
  - Com `GradleProject`, usa `getConfiguration("compileClasspath")` e `findResolvedDependency("org.springframework.cloud", "spring-cloud-starter-sleuth")`.
- **Visitor:** `Preconditions.check` com um visitor que devolve `SearchResult.found(tree)` quando o `JavaProject` do arquivo está no conjunto; o `AddSpringProperty` em si não mudou.
- `displayName`/`description` intactos, e nenhuma mudança em `spring-cloud-2022.yml`.

### Testes (5/5 passando)
- `addLoggingPatternWhenUsingSleuth` e `doNotAddWhenNotUsingSleuth` seguem verdes, agora embrulhados em `mavenProject(...)`.
- `onlyAddToModuleUsingSleuth`: multimódulo Maven com `sleuth-app` e `plain-app`; só o primeiro recebe `logging.pattern.level`.
- `gradleProjectUsingSleuth` e `gradleProjectNotUsingSleuth`: `buildGradle` com `spec.beforeRecipe(withToolingApi())`, com e sem `spring-cloud-starter-sleuth`.

### Passos (todos concluídos)
1. Análise completa e código proposto: feitos.
2. Branch `b3-sleuth-logging-pattern-per-project` criado a partir da `main`.
3. Comentário `I'd like to take B3` na #1201 em 10/11/2026.
4. Implementação à mão da receita e dos testes.
5. Validação local (5/5).
6. Autorrevisão com a skill `review-recipe-pr` contra `upstream/main`.
7. PR #1283 aberta, revisada e mergeada por `timtebeek` como `3231afb3` em 11/11/2026.
8. Comentário na #1201 avisando que o B3 foi resolvido em #1283: feito em 11/11/2026.

### Critério de pronto
- Testes multimódulo + Gradle novos passam; testes antigos verdes.
- O acumulador guarda `Set<JavaProject>` (valores, não árvores).
- Diff restrito a `AddLoggingPatternLevelForSleuth.java` e `AddLoggingPatternLevelForSleuthTest.java`.

---

## Não fazer (nas quatro tarefas)
- Não alterar nada sem autorização explícita do Dav: arquivos (inclusive este plano), branches, commits, push, comentários e PRs. Ver "Regras de contribuição".
- Não mencionar IA/agente (`Generated with...`, `Co-Authored-By:` de bot) nem usar travessões típicos de IA (`—` / `–`) em commits, PRs ou comentários; escrever sempre em tom humano e direto, seguindo o padrão do histórico do repositório.
- Não reformatar arquivos inteiros, não atualizar dependências fora do escopo da tarefa e não "aproveitar" para corrigir outras coisas.
- Não criar branches de contribuição a partir de `planos` — sempre a partir de `main` (ver "Este arquivo (branch `planos`)" nas Regras de contribuição).
- Não abrir PR antes de comentar na issue. Nas tarefas A, B, C e D o comentário já foi feito.
- Não inventar APIs. Se não tiver certeza de um método (`getOutputPath()`, API do `GradleProject`), procure no código-fonte da dependência antes de usar.
