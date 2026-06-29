<div align="center">

☕

# Java Clean Architecture

**Exemplo didático de Clean Architecture em Java/Spring Boot com domínio, casos de uso e adapters separados.**

<br />

[![Repositório público](https://img.shields.io/badge/repo-público-2ea44f?style=flat-square&logo=github&logoColor=white)](https://github.com/oadcavalcante/java-clean-architecture)

<br />

[![Java 17](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logoColor=fff&logo=openjdk)](https://github.com/oadcavalcante/java-clean-architecture) [![Spring Boot 3.2](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=flat-square&logoColor=fff&logo=springboot)](https://github.com/oadcavalcante/java-clean-architecture) [![Spring Web](https://img.shields.io/badge/Spring_Web-555555?style=flat-square)](https://github.com/oadcavalcante/java-clean-architecture) [![Spring Data JPA](https://img.shields.io/badge/Spring_Data_JPA-555555?style=flat-square)](https://github.com/oadcavalcante/java-clean-architecture)

[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logoColor=fff&logo=postgresql)](https://github.com/oadcavalcante/java-clean-architecture)

[![Maven](https://img.shields.io/badge/Maven-C71A36?style=flat-square&logoColor=fff&logo=apachemaven)](https://github.com/oadcavalcante/java-clean-architecture) [![JUnit 5](https://img.shields.io/badge/JUnit-25A162?style=flat-square&logoColor=fff&logo=junit5)](https://github.com/oadcavalcante/java-clean-architecture)

<br />

[Stack completa ↓](#stack)

<br />

[Documentação](https://github.com/oadcavalcante/java-clean-architecture/blob/main/README.md) · [Deploy](#deploy) · [API](http://localhost:8080/usuarios) · [Issues](https://github.com/oadcavalcante/java-clean-architecture/issues)

</div>

## Features

- ✨ Camadas domain, application, adapters e infrastructure
- 🚀 Casos de uso CriarUsuario e ListarUsuarios desacoplados do framework
- ⚡ Ports e gateways para persistência (JPA e arquivo)
- 🎯 Controller REST /usuarios sem regra de negócio no adapter
- 🔧 Testes unitários de domínio e aplicação

## Getting Started

| Ambiente | Comando / Link |
|----------|----------------|
| Primeira vez | `./mvnw spring-boot:run` |
| Documentação | [README](https://github.com/oadcavalcante/java-clean-architecture/blob/main/README.md) |
| Produção | N/A |

## Stack

- **Backend:** Java 17, Spring Boot 3.2, Spring Web, Spring Data JPA
- **Dados:** PostgreSQL
- **Infra / DevOps:** Maven, JUnit 5

---

<!-- README.md em HTML (compatível com renderização do GitHub) -->

<h1>Java Clean Architecture (Spring Boot) — Exemplo inspirado em Uncle Bob</h1> <p> Este repositório é um <strong>projeto exemplo em Java + Spring Boot</strong> com o objetivo de demonstrar, na prática, a <strong>Clean Architecture</strong> descrita por <strong>Robert C. Martin (Uncle Bob)</strong>. </p> <p> A ideia central é manter o <strong>domínio</strong> e os <strong>casos de uso</strong> independentes de frameworks, banco de dados e detalhes de infraestrutura — e fazer com que essas dependências apontem <strong>sempre para dentro</strong> (<em>Dependency Rule</em>). </p> <hr/> <h2>Objetivos do projeto</h2> <ul> <li>Servir como <strong>referência didática</strong> de Clean Architecture em Java</li> <li>Separar claramente: <ul> <li><strong>Entidades (Domínio)</strong></li> <li><strong>Casos de uso (Application / Use Cases)</strong></li> <li><strong>Interfaces (Controllers, Presenters, Gateways)</strong></li> <li><strong>Infraestrutura (Spring, DB, REST, etc.)</strong></li> </ul> </li> <li>Facilitar: <ul> <li><strong>testes unitários</strong> sem Spring</li> <li>troca de banco/infra sem tocar no domínio</li> <li>manutenção e evolução do sistema</li> </ul> </li> </ul> <hr/> <h2>Conceitos-chave (Clean Architecture)</h2> <h3>Regra da dependência (Dependency Rule)</h3> <blockquote> Código em camadas externas <strong>pode depender</strong> de camadas internas, mas <strong>nunca o contrário</strong>. </blockquote> <p> <strong>Mais interno →</strong> mais estável / mais importante<br/> <strong>Mais externo →</strong> mais volátil / detalhes </p> <p><strong>Camadas típicas:</strong></p> <ol> <li><strong>Entities (Domínio)</strong></li> <li><strong>Use Cases (Regras de aplicação)</strong></li> <li><strong>Interface Adapters (Controllers / Gateways / Presenters)</strong></li> <li><strong>Frameworks &amp; Drivers (Spring, DB, Web, etc.)</strong></li> </ol> <hr/> <h2>Estrutura sugerida do projeto</h2> <p> <em>A estrutura pode variar, mas o importante é respeitar as dependências.</em> </p> <pre><code>src/main/java └── br/com/seuapp ├── domain │ ├── entity │ └── exception │ ├── application │ ├── usecase │ ├── port │ │ ├── in │ │ └── out │ └── dto │ ├── adapters │ ├── in │ │ └── web │ │ ├── controller │ │ └── request │ └── out │ ├── persistence │ │ ├── entity │ │ ├── repository │ │ └── mapper │ └── external │ └── infrastructure ├── config └── boot └── Application.java</code></pre> <h3>O que vai em cada camada?</h3> <h4><code>domain/</code></h4> <ul> <li>Regras mais puras do negócio</li> <li>Entidades, VOs, validações essenciais</li> <li>Sem dependência de Spring, JPA, Jackson, etc.</li> </ul> <h4><code>application/</code></h4> <ul> <li>Casos de uso (orquestram o domínio)</li> <li>Portas (interfaces) para entrada/saída: <ul> <li><code>port/in</code>: o que o sistema oferece (ex: <code>CriarPedidoUseCase</code>)</li> <li><code>port/out</code>: o que o sistema precisa (ex: <code>PedidoRepositoryPort</code>)</li> </ul> </li> </ul> <h4><code>adapters/</code></h4> <ul> <li>Implementações dos ports</li> <li><strong>Inbound</strong>: controllers REST, handlers, schedulers</li> <li><strong>Outbound</strong>: persistência (JPA), clients HTTP, mensageria, etc.</li> </ul> <h4><code>infrastructure/</code></h4> <ul> <li>Configuração do Spring, beans, wiring, properties</li> <li>É onde “mora” o framework</li> </ul> <hr/> <h2>Fluxo de chamada (exemplo)</h2> <p> <code>HTTP Request → Controller (adapter/in) → UseCase (application) → Port/out → Adapter/out (JPA, API externa, etc.)</code> </p> <p> O <strong>UseCase</strong> não conhece Spring nem JPA.<br/> Ele depende apenas de <strong>interfaces (ports)</strong>. </p> <hr/> <h2>Tecnologias</h2> <ul> <li>Java (LTS recomendado)</li> <li>Spring Boot</li> <li>(Opcional) Spring Web / Validation</li> <li>(Opcional) Spring Data JPA</li> <li>(Opcional) H2/PostgreSQL</li> <li>JUnit 5 + Mockito (testes)</li> </ul> <p><em>Observação: Frameworks ficam nas camadas externas.</em></p> <hr/> <h2>Como rodar</h2> <h3>Pré-requisitos</h3> <ul> <li>Java instalado (preferencialmente LTS)</li> <li>Maven ou Gradle</li> </ul> <h3>Executar</h3> <pre><code>./mvnw spring-boot:run</code></pre> <p>ou</p> <pre><code>./gradlew bootRun</code></pre> <hr/> <h2>Testes</h2> <p> A maior vantagem aqui é que você consegue testar os <strong>Use Cases</strong> sem subir Spring. </p> <h3>Rodar testes</h3> <pre><code>./mvnw test</code></pre> <p>ou</p> <pre><code>./gradlew test</code></pre> <h3>O que testar em cada camada?</h3> <ul> <li><code>domain/</code>: validações e regras puras (sem mocks quase sempre)</li> <li><code>application/</code>: casos de uso (mockando apenas <code>port/out</code>)</li> <li><code>adapters/</code>: controllers com testes de slice (ex: <code>@WebMvcTest</code>) ou integração</li> <li><code>infrastructure/</code>: testes de integração com DB real/container, quando necessário</li> </ul> <hr/> <h2>Convenções e boas práticas</h2> <ul> <li><strong>DTO não é entidade</strong>: entidade é domínio, DTO é transporte.</li> <li><strong>Controller não contém regra de negócio</strong>: apenas traduz entrada/saída.</li> <li><strong>Persistência não “vaza” para dentro</strong>: <ul> <li>nada de <code>@Entity</code> no domínio</li> <li>nada de <code>JpaRepository</code> dentro de <code>application</code></li> </ul> </li> <li><strong>Mapper</strong> para converter: <ul> <li>Request → Input DTO/Command</li> <li>Domain ↔ Persistence Entity</li> <li>Domain → Response DTO</li> </ul> </li> </ul> <hr/> <h2>Exemplos de “cheiros ruins” (o que evitar)</h2> <ul> <li>Use case anotado com <code>@Service</code> (até pode, mas preferível isolar wiring)</li> <li>Domínio usando <code>@Entity</code>, <code>@Autowired</code>, <code>ResponseEntity</code>, <code>Pageable</code>, etc.</li> <li>Controller chamando direto <code>JpaRepository</code></li> <li>Regras de negócio dentro do controller</li> </ul> <hr/> <h2>Referências</h2> <ul> <li>Robert C. Martin — <em>Clean Architecture: A Craftsman’s Guide to Software Structure and Design</em></li> <li>The Clean Architecture (artigos e talks do Uncle Bob)</li> </ul> <hr/> <h2>Licença</h2> <p> Use este projeto como base para estudos, POCs e testes.<br/> Se você for publicar ou usar em produção, revise as dependências, validações e segurança conforme sua necessidade. </p>
