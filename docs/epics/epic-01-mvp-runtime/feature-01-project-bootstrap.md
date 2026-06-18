# Feature 1: Project Bootstrap

## Feature Goal

Create the repository, solution structure, documentation layout, local scripts, and optional Docker Compose foundation.

## Design Patterns / Engineering Concepts

- Clean Architecture
- Ports and Adapters
- Infrastructure as code
- Environment parity

---

## PBI 1.1: Initialize Repository Structure

### Requirement

Create the monorepo structure for C#, Python, docs, contracts, data, infrastructure, and scripts.

### Checklist

- [X] Create `README.md`.
- [X] Create `docs/`.
- [x] Create `src/`.
- [x] Create `tests/`.
- [x] Create `python/`.
- [x] Create `contracts/`.
- [x] Create `data/`.
- [x] Create `infra/docker/`.
- [x] Create `scripts/`.
- [x] Create `.gitignore`.
- [x] Ensure generated data files are ignored by Git.
- [x] Document `main`, `dev`, and `feature/pbi-xxx` branch workflow.

### Acceptance Criteria

- [x] Repository contains all required top-level directories.
- [x] `data/` exists but generated data files are ignored.
- [x] `README.md` explains project purpose and runtime modes.
- [x] `docs/ROADMAP_INDEX.md` exists.
- [x] Branch workflow is documented.

---

## PBI 1.2: Create C# Solution Structure

### Requirement

Create the initial .NET solution and projects.

### Projects

```text
QuantLifecycleEngine.Host
QuantLifecycleEngine.Domain
QuantLifecycleEngine.Application
QuantLifecycleEngine.Infrastructure
QuantLifecycleEngine.Backtesting
```

### Checklist

- [x] Create `QuantLifecycleEngine.sln`.
- [x] Create `QuantLifecycleEngine.Host`.
- [x] Create `QuantLifecycleEngine.Domain`.
- [x] Create `QuantLifecycleEngine.Application`.
- [x] Create `QuantLifecycleEngine.Infrastructure`.
- [x] Create `QuantLifecycleEngine.Backtesting`.
- [x] Add all projects to the solution.
- [x] Configure project references.

### Acceptance Criteria

- [x] `dotnet build` succeeds.
- [x] Domain does not depend on Application, Infrastructure, or Backtesting.
- [x] Application depends on Domain.
- [x] Infrastructure depends on Application and Domain.
- [x] Host depends on Application and Infrastructure.
- [x] Backtesting depends on Application and Domain.

---

## PBI 1.3: Create Test Projects

### Requirement

Create test projects for domain, application, infrastructure, and backtesting.

### Checklist

- [x] Create `QuantLifecycleEngine.Domain.Tests`.
- [x] Create `QuantLifecycleEngine.Application.Tests`.
- [x] Create `QuantLifecycleEngine.Infrastructure.Tests`.
- [x] Create `QuantLifecycleEngine.Backtesting.Tests`.
- [x] Add test projects to the solution.
- [x] Add placeholder tests.
- [x] Confirm all tests can run locally.

### Acceptance Criteria

- [x] `dotnet test` succeeds.
- [x] Each test project has at least one placeholder test.
- [x] Test project references are correct.
- [x] Tests do not require broker connection.

---

## PBI 1.4: Add Docker Compose Foundation

### Requirement

Add Docker Compose foundation for optional local infrastructure.

### Checklist

- [x] Add `docker-compose.yml` at repository root.
- [x] Add `.dockerignore`.
- [x] Add `infra/docker/kafka/README.md`.
- [x] Use Compose profiles so Kafka is not started by default.
- [x] Document startup and shutdown commands.
- [x] Confirm MVP can run without Docker Compose.

### Acceptance Criteria

- [x] `docker compose config` succeeds.
- [x] Kafka services are disabled by default or clearly marked as enrichment-only.
- [x] README documents when Docker Compose is needed.
- [x] MVP backtest mode does not require Docker Compose.
- [x] MVP paper/live mode does not require Docker Compose.
