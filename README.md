# **Aplicação Flask com Docker e CI/CD Automatizado**

![GitHub](https://img.shields.io/badge/Docker-Supported-blue) ![Python](https://img.shields.io/badge/Python-3.9-blue) ![Flask](https://img.shields.io/badge/Flask-2.x-blue) ![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-blue)

Este projeto demonstra como criar uma aplicação Flask simples, containerizá-la com Docker e automatizar o processo de construção e envio da imagem para o Docker Hub usando GitHub Actions. O objetivo é fornecer um exemplo claro e funcional de como integrar Docker com pipelines CI/CD.

---

## **Índice**

1. [Descrição do Projeto](#descrição-do-projeto)
2. [Tecnologias Utilizadas](#tecnologias-utilizadas)
3. [Pré-requisitos](#pré-requisitos)
4. [Estrutura do Projeto](#estrutura-do-projeto)
5. [Passo a Passo para Executar Localmente](#passo-a-passo-para-executar-localmente)
6. [Configuração do Pipeline CI/CD](#configuração-do-pipeline-cicd)
7. [Como Funciona o Workflow GitHub Actions](#como-funciona-o-workflow-github-actions)
8. [Contribuição](#contribuição)
9. [Licença](#licença)

---

## **Descrição do Projeto**

Este projeto consiste em uma aplicação Flask simples que exibe "Olá, mundo!" quando acessada. A aplicação é containerizada usando Docker e automatizada com GitHub Actions para construir e enviar imagens Docker para o Docker Hub sempre que houver alterações no código.

---

## **Tecnologias Utilizadas**

- **Python 3.9**: Linguagem de programação utilizada para desenvolver a aplicação Flask.
- **Flask**: Framework web minimalista para Python.
- **Docker**: Plataforma usada para criar, implantar e executar a aplicação em containers.
- **GitHub Actions**: Ferramenta de automação integrada ao GitHub para criar pipelines CI/CD.
- **Docker Hub**: Registro público para armazenar e compartilhar imagens Docker.

---

## **Pré-requisitos**

Antes de iniciar, certifique-se de ter as seguintes ferramentas instaladas:

- **Git**: Para clonar o repositório.
- **Docker**: Para executar a aplicação localmente (opcional).
- **Conta no Docker Hub**: Para armazenar as imagens geradas pelo pipeline.
- **Conta no GitHub**: Para hospedar o repositório e configurar o pipeline CI/CD.

---

## **Estrutura do Projeto**

Aqui está a estrutura básica do projeto:

```
flask-docker-ci-cd/
│
├── app.py              # Código da aplicação Flask
├── requirements.txt    # Dependências Python
├── Dockerfile          # Instruções para criar a imagem Docker
├── .github/
│   └── workflows/
│       └── docker.yml  # Configuração do GitHub Actions
└── README.md           # Documentação do projeto
```

---

## **Passo a Passo para Executar Localmente**

### **Passo 1: Clone o Repositório**

Clone este repositório para sua máquina local:

```bash
git clone https://github.com/seu-usuario/flask-docker-ci-cd.git
cd flask-docker-ci-cd
```

### **Passo 2: Construa a Imagem Docker**

Construa a imagem Docker localmente usando o comando abaixo:

```bash
docker build -t flask-app .
```

### **Passo 3: Execute o Container**

Execute o container Docker na porta `5000`:

```bash
docker run -p 5000:5000 flask-app
```

### **Passo 4: Acesse a Aplicação**

Abra o navegador e acesse:

```
http://localhost:5000
```

Você deverá ver a mensagem:

```
Olá, mundo!
```

---

## **Configuração do Pipeline CI/CD**

O pipeline CI/CD é configurado usando **GitHub Actions** para automatizar a construção e o envio da imagem Docker para o Docker Hub.

### **Passo 1: Crie um Arquivo `.github/workflows/docker.yml`**

Crie o arquivo `.github/workflows/docker.yml` com o seguinte conteúdo:

```yaml
name: Docker Build & Push

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Login to Docker Hub
        run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin

      - name: Build Docker Image
        run: docker build -t myusername/myapp:latest .

      - name: Push to Docker Hub
        run: docker push myusername/myapp:latest
```

Substitua `myusername` e `myapp` pelos seus dados do Docker Hub.

### **Passo 2: Configure Secrets no GitHub**

Para que o pipeline funcione, você precisa configurar suas credenciais do Docker Hub como segredos no GitHub.

1. Acesse o seu repositório no GitHub.
2. Vá para **Settings > Secrets and variables > Actions**.
3. Clique em **New repository secret** e adicione os seguintes segredos:
   - Nome: `DOCKER_USERNAME`
     - Valor: Seu nome de usuário do Docker Hub.
   - Nome: `DOCKER_PASSWORD`
     - Valor: Sua senha ou token de acesso do Docker Hub.

### **Passo 3: Faça Push para o GitHub**

Faça commit e push das alterações para a branch `main`:

```bash
git add .
git commit -m "Adiciona workflow do GitHub Actions"
git push origin main
```

---

## **Como Funciona o Workflow GitHub Actions**

O arquivo `docker.yml` define um pipeline que realiza as seguintes etapas:

1. **Checkout do Repositório**:
   - Faz o download do código do repositório.

2. **Login no Docker Hub**:
   - Usa as credenciais armazenadas nos secrets para autenticar no Docker Hub.

3. **Construção da Imagem Docker**:
   - Constrói a imagem Docker com base no `Dockerfile`.

4. **Envio da Imagem para o Docker Hub**:
   - Envia a imagem construída para o Docker Hub.

---

## **Contribuição**

Contribuições são bem-vindas! Siga estas etapas:

1. Faça um fork deste repositório.
2. Crie uma nova branch:
   ```bash
   git checkout -b feature/nova-funcionalidade
   ```
3. Faça suas alterações e commit:
   ```bash
   git commit -m "Adiciona nova funcionalidade"
   ```
4. Envie suas alterações:
   ```bash
   git push origin feature/nova-funcionalidade
   ```
5. Abra um Pull Request neste repositório.

---

## **Licença**

Este projeto está licenciado sob a **MIT License**. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

## **Contato**

Se tiver dúvidas ou sugestões, entre em contato:

- **Nome**: Luan Castro
- **Email**: luandecastrosilva@gmail.com
- **LinkedIn**: [linkedin.com/in/luancastrosilva](https://www.linkedin.com/in/luancastrosilva/)
- **GitHub**: [github.com/luangitdev](https://github.com/luangitdev)