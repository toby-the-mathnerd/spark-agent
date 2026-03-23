# skill: devops
# purpose: Infrastructure, deployment, and system configuration
# triggers: Task type = "devops"

## RPOLES Integration

DevOps tasks use a **compressed RPOLES flow** — infrastructure work often needs
less upfront design and more iterative validation.

| Phase | Skill | Output |
|-------|------|--|
| Review | dev-review | Requirements understood, scope defined |
| Plan | dev-plan | Deployment strategy, environment setup |
| Outline | — | Often skipped — infrastructure is declarative |
| Locate | dev-locate | Dependencies, existing infrastructure patterns |
| Implement | dev-implement | Infrastructure as code |
| Test | dev-test | Validation, integration tests |
| Ship | dev-ship | Deployed, documented |

## Phase-Specific Actions

### REVIEW — Understand Infrastructure Requirements

```bash
# 1. Read task requirements
# 2. Identify target environments
# 3. Note any compliance/security requirements
# 4. List dependencies on existing infrastructure
```

**Key questions:**
- What environment(s)? (dev, staging, prod)
- What's being deployed? (service, config, pipeline)
- What are the constraints? (security, compliance, cost)
- What does success look like?

**Output:** Infrastructure requirements in task file

```markdown
## Infrastructure Requirements

**Target:** [environment(s)]

**Components:**
- [component 1] - [purpose]
- [component 2] - [purpose]

**Constraints:**
- [constraint 1]
- [constraint 2]

**Dependencies:**
- [existing infrastructure]
```

### PLAN — Design Deployment Strategy

```bash
# 1. Choose infrastructure-as-code approach
# 2. Define deployment steps
# 3. Plan rollback strategy
# 4. Identify validation points
```

**Output:** Deployment plan in task file

```markdown
## Deployment Plan

**Approach:** [terraform/ansible/k8s/docker]

**Steps:**
1. [setup phase]
2. [deploy phase]
3. [validate phase]

**Rollback:**
- [rollback steps]

**Validation:**
- [check 1]
- [check 2]
```

### LOCATE — Find Infrastructure Patterns

```bash
# Check existing infrastructure
ls ~/claude-workspace/infra/
ls ~/claude-workspace/.github/workflows/
ls ~/claude-workspace/deploy/

# Review similar deployments
grep -r "terraform" ~/claude-workspace/ --include="*.tf" | head -10
grep -r "ansible" ~/claude-workspace/ --include="*.yml" | head -10
```

**Output:** Infrastructure patterns identified

### IMPLEMENT — Create Infrastructure

```bash
# 1. Create infrastructure files
# 2. Use declarative approach where possible
# 3. Document each component
# 4. Commit incrementally

git add .
git commit -m "[task/NNN] infra: add [component]"
git push
```

**Common artifacts:**
- Terraform `.tf` files
- Ansible playbooks `.yml`
- Kubernetes manifests `.yaml`
- Dockerfiles
- CI/CD pipelines `.github/workflows/`

### TEST — Validate Infrastructure

```bash
# 1. Validate syntax
terraform validate
ansible-lint playbooks/
kubeval manifests/

# 2. Plan changes (no-apply)
terraform plan

# 3. Test in dev/staging first
# 4. Verify connectivity/config
```

**Output:** Validation passed, changes ready

### SHIP — Deploy and Document

```bash
# 1. Apply to target environment
# 2. Verify deployment
# 3. Document in task file
# 4. Move task to done/
```

## Common DevOps Patterns

### CI/CD Pipeline
```yaml
# .github/workflows/<name>.yml
name: <pipeline>
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run tests
        run: npm test
      - name: Deploy
        if: github.ref == 'refs/heads/main'
        run: ./deploy.sh
```

### Dockerfile
```dockerfile
FROM <base-image>
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

### Kubernetes Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: <app-name>
spec:
  replicas: 3
  selector:
    matchLabels:
      app: <app-name>
  template:
    metadata:
      labels:
        app: <app-name>
    spec:
      containers:
      - name: <app-name>
        image: <image>:<tag>
        ports:
        - containerPort: 3000
```

## Artifacts

| Artifact | Location | When |
|---------|---..----|-----.-|
| Infrastructure files | ~/claude-workspace/infra/ | Implement |
| Pipeline configs | .github/workflows/ | Implement |
| Dockerfiles | ~/claude-workspace/ | Implement |
| Validation results | task file | Test |
| Deployment docs | task file | Ship |

## Checkpoints

```bash
checkpoint --phase review --description "Infrastructure requirements understood" --next "Proceed to planning"
checkpoint --phase locate --description "Infrastructure patterns identified" --next "Proceed to implementation"
checkpoint --phase implement --description "Infrastructure created" --next "Proceed to validation"
checkpoint --phase test --description "Infrastructure validated" --next "Proceed to deployment"
checkpoint --phase ship --description "Deployed and documented" --next "Task complete"
```

## Success Criteria

- [ ] Infrastructure is declarative and versioned
- [ ] Validation passes
- [ ] Deployment successful
- [ ] Rollback documented
- [ ] Documentation updated
- [ ] Task file complete with Result + Agent Log

---

*DevOps is infrastructure RPOLES. Review→Plan→Locate→Implement→Test→Ship.*
