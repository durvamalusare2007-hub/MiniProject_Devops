# DevOps Mini Projects

A collection of 6 hands-on mini projects covering core DevOps concepts — from Infrastructure as Code and containerization to CI/CD pipelines and automated testing.


## MiniProject 1 — Terraform Local File Demo

**Directory:** `terraform-demo/`

A beginner-level Terraform project that provisions a local text file using the `hashicorp/local` provider. Introduces core Terraform concepts like providers, resources, and state management.

### What It Does
- Configures the `hashicorp/local` provider (`~> 2.5`)
- Creates a local file `hello_terraform.txt` with a welcome message using a `local_file` resource

### Files
```
terraform-demo/
├── main.tf                  # Terraform configuration
├── terraform.tfstate        # State file
└── .terraform.lock.hcl      # Provider lock file
```

### How to Run
```bash
terraform init
terraform plan
terraform apply
```

After `apply`, a file named `hello_terraform.txt` will be created in the project directory.

---

## MiniProject 2 — Nginx Docker + GitHub Actions CI

**Directory:** `nginx-demo/`

A Dockerized static Nginx web server with a GitHub Actions CI/CD pipeline that automatically builds, tests, and deploys the container on every push to `main`.

### What It Does
- Serves a custom `index.html` via Nginx inside a Docker container
- GitHub Actions pipeline: builds the image → runs the container → health-checks with `curl` → tears down

### Files
```
nginx-demo/
├── Dockerfile                        # Nginx image with custom HTML
├── index.html                        # Static web page
└── .github/workflows/ci.yml          # CI/CD pipeline
```

### How to Run Locally
```bash
docker build -t my-nginx .
docker run -d -p 8080:80 my-nginx
# Visit http://localhost:8080
```

### CI Pipeline Stages
1. **Checkout** code
2. **Build** Docker image
3. **Run** container on port 8080
4. **Test** with `curl -I http://localhost:8080`
5. **Stop & clean up** container
6. **Deploy** step (placeholder)

---

## MiniProject 3 — Python Calculator with Unit Tests

**Directory:** `project/`

A minimal Python calculator module with unit tests written using `pytest`. Demonstrates test-driven development (TDD) fundamentals.

### What It Does
- Implements `add(a, b)` and `subtract(a, b)` functions
- Tests both functions with positive, negative, and zero-value cases using `pytest`

### Files
```
project/
├── calculator.py           # Core calculator functions
└── test_calculator.py      # Pytest unit tests
```

### How to Run
```bash
pip install pytest
pytest test_calculator.py -v
```

### Test Cases
| Test | Assertions |
|------|-----------|
| `test_add` | `4+5=9`, `-1+1=0` |
| `test_sub` | `10-5=5`, `0-1=-1` |

---

## MiniProject 4 — Multi-Service Docker Compose

**Directory:** `DockerComposer/`

A Docker Compose setup that launches two Nginx services simultaneously, each serving different HTML content on different ports. Introduces multi-container orchestration.

### What It Does
- **web1** — serves `index.html` on port `8080`
- **web2** — serves a default Nginx page on port `6060`
- Uses volume mounts to inject custom HTML into web1

### Files
```
DockerComposer/
├── docker-compose.yaml      # Defines web1 and web2 services
└── html/
    ├── index.html           # Content served by web1
    └── main.html            # Additional HTML page
```

### How to Run
```bash
docker compose up -d
# web1 → http://localhost:8080
# web2 → http://localhost:6060
```

---

## MiniProject 5 — Python Docker App

**Directory:** `project-06-docker-simple/`

The simplest possible Dockerized Python application. A great starting point for understanding how to containerize any Python script.

### What It Does
- Runs a Python script that prints `Hello Docker Project 06`
- Uses the official `python:3.9` base image

### Files
```
project-06-docker-simple/
├── app.py        # Python application
└── Dockerfile    # Container definition
```

### How to Run
```bash
docker build -t docker-simple .
docker run docker-simple
# Output: Hello Docker Project 06
```

---

## MiniProject 6 — Terraform IaC + CI/CD Pipeline

**Directory:** `iac-cicd-lab/`

An end-to-end Infrastructure as Code lab combining Terraform with a full GitHub Actions CI/CD pipeline. The pipeline runs on every pull request, validates the Terraform code, generates a plan, and posts the plan output as a PR comment.

### What It Does
- Provisions a local file using the `hashicorp/local` Terraform provider
- GitHub Actions pipeline triggers on pull requests to `main` and runs the full Terraform workflow

### Files
```
iac-cicd-lab/
├── main.tf                                  # Terraform IaC config
├── .terraform.lock.hcl                      # Provider lock file
└── .github/workflows/terraform-ci.yml       # CI/CD pipeline
```

### How to Run Locally
```bash
terraform init
terraform fmt
terraform validate
terraform plan
```

### CI Pipeline Stages
1. **Checkout** code
2. **Setup Terraform** (v1.7.0)
3. **Format check** — `terraform fmt -check -recursive`
4. **Init** — `terraform init -backend=false`
5. **Validate** — `terraform validate`
6. **Plan** — runs `terraform plan` and saves output
7. **PR Comment** — posts plan result (✅ or ❌) as a GitHub PR comment
8. **Fail gate** — exits with error if the plan failed



## Learning Path

These projects are designed to be completed in order:

```
Project 3 (Python + Testing)
    ↓
Project 5 (Docker basics)
    ↓
Project 2 (Docker + CI)
    ↓
Project 4 (Docker Compose)
    ↓
Project 1 (Terraform basics)
    ↓
Project 6 (Terraform + CI/CD)
```

---

## Author

DevOps Mini Projects — Hands-on labs for learning modern DevOps tooling.
