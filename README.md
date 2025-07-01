# ci-cd-docker-github-actions
## CI/CD com GitHub Actions para Docker
### 🎯 Objetivo
Automatizar a criação e publicação da imagem Docker de uma aplicação Node.js no Docker Hub, sempre que houver `push` no repositório.

📁 Estrutura do projeto
```
lab-03-cicd-docker-github-actions/
├── .github/
│   └── workflows/
│       └── docker-build.yml
├── Dockerfile
├── .dockerignore
├── package.json
├── package-lock.json
├── index.js
├── README.md
```
🧱 Workflow: docker-build.yml
```
name: Build and Push Docker Image

on:
  push:
    branches: [ "main" ]

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v3

    - name: Log in to Docker Hub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}

    - name: Build and push image
      uses: docker/build-push-action@v5
      with:
        context: .
        push: true
        tags: tse/docker-node-app:latest
```
🔐 Secrets no GitHub
Você precisa adicionar 2 segredos no repositório GitHub:

1. `DOCKER_USERNAME` → seu usuário do Docker Hub
2. `DOCKER_PASSWORD` → seu token de acesso ou senha

Acesse seu repositório > Settings > Secrets > Actions

▶️ Fluxo de execução
1. Clone o projeto ou suba no seu repositório
2. Adicione os secrets
3. Faça um `git push` na branch main
4. O GitHub Actions irá:
  - Fazer checkout do código
  - Fazer login no Docker Hub
  - Buildar a imagem com Dockerfile
  - Publicar no Docker Hub

✅ Resultado esperado
- Imagem Docker publicada automaticamente a cada git push
- GitHub Actions funcionando como pipeline de CI/CD
- Projeto pronto para ser integrado ao deploy via Terraform ou Kubernetes

Teste