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

- [ ] Create `README.md`.
- [ ] Create `docs/`.
- [ ] Create `src/`.
- [ ] Create `tests/`.
- [ ] Create `python/`.
- [ ] Create `contracts/`.
- [ ] Create `data/`.
- [ ] Create `infra/docker/`.
- [ ] Create `scripts/`.
- [ ] Create `.gitignore`.
- [ ] Ensure generated data files are ignored by Git.
- [ ] Document `main`, `dev`, and `feature/pbi-xxx` branch workflow.

### Acceptance Criteria

- [ ] Repository contains all required top-level directories.
- [ ] `data/` exists but generated data files are ignored.
- [ ] `README.md` explains project purpose and runtime modes.
- [ ] `docs/ROADMAP_INDEX.md` exists.
- [ ] Branch workflow is documented.

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

- [ ] Create `QuantLifecycleEngine.sln`.
- [ ] Create `QuantLifecycleEngine.Host`.
- [ ] Create `QuantLifecycleEngine.Domain`.
- [ ] Create `QuantLifecycleEngine.Application`.
- [ ] Create `QuantLifecycleEngine.Infrastructure`.
- [ ] Create `QuantLifecycleEngine.Backtesting`.
- [ ] Add all projects to the solution.
- [ ] Configure project references.

### Acceptance Criteria

- [ ] `dotnet build` succeeds.
- [ ] Domain does not depend on Application, Infrastructure, or Backtesting.
- [ ] Application depends on Domain.
- [ ] Infrastructure depends on Application and Domain.
- [ ] Host depends on Application and Infrastructure.
- [ ] Backtesting depends on Application and Domain.

---

## PBI 1.3: Create Test Projects

### Requirement

Create test projects for domain, application, infrastructure, and backtesting.

### Checklist

- [ ] Create `QuantLifecycleEngine.Domain.Tests`.
- [ ] Create `QuantLifecycleEngine.Application.Tests`.
- [ ] Create `QuantLifecycleEngine.Infrastructure.Tests`.
- [ ] Create `QuantLifecycleEngine.Backtesting.Tests`.
- [ ] Add test projects to the solution.
- [ ] Add placeholder tests.
- [ ] Confirm all tests can run locally.

### Acceptance Criteria

- [ ] `dotnet test` succeeds.
- [ ] Each test project has at least one placeholder test.
- [ ] Test project references are correct.
- [ ] Tests do not require broker connection.

---

## PBI 1.4: Add Docker Compose Foundation

### Requirement

Add Docker Compose foundation for optional local infrastructure.

### Checklist

- [ ] Add `docker-compose.yml` at repository root.
- [ ] Add `.dockerignore`.
- [ ] Add `infra/docker/kafka/README.md`.
- [ ] Use Compose profiles so Kafka is not started by default.
- [ ] Document startup and shutdown commands.
- [ ] Confirm MVP can run without Docker Compose.

### Acceptance Criteria

- [ ] `docker compose config` succeeds.
- [ ] Kafka services are disabled by default or clearly marked as enrichment-only.
- [ ] README documents when Docker Compose is needed.
- [ ] MVP backtest mode does not require Docker Compose.
- [ ] MVP paper/live mode does not require Docker Compose.
