# 👨‍🏫 Usando o K8sGPT como um Professor Particular para a CKA

Este repositório documenta uma metodologia prática para usar o **K8sGPT**, uma ferramenta de IA para Kubernetes, como um acelerador de aprendizado para a certificação **Certified Kubernetes Administrator (CKA)**.

## A Filosofia: O Professor vs. A Muleta

O exame CKA testa a **sua** habilidade de diagnosticar e resolver problemas rapidamente. O uso de uma ferramenta de IA pode ser uma faca de dois gumes:

- **A Muleta (O Jeito Errado):** Usar o \`k8sgpt analyze\` como primeira opção ao encontrar um erro. Isso impede a prática dos comandos essenciais (\`kubectl describe\`, \`logs\`, etc.) e a construção da "memória muscular" necessária para a prova.

- **O Professor (O Jeito Certo):** Usar o K8sGPT como um "revisor" do seu próprio diagnóstico. A metodologia é:
    1. Encontre um problema no lab.
    2. Tente diagnosticar e resolver **manualmente**, usando os comandos padrão do \`kubectl\`.
    3. **Só então**, rode o \`k8sgpt analyze --explain\` para validar seu raciocínio, obter uma explicação mais profunda ou descobrir um novo ângulo que você não tinha visto.

## ⚙️ Guia de Instalação e Configuração (Debian/Ubuntu)

### 1. Instalação via APT
\`\`\`bash
# Adiciona a chave do repositório
curl -fsSL https://download.opensuse.org/repositories/home:/k8sgpt-ai:/stable/xUbuntu_22.04/Release.key | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/k8sgpt.gpg

# Adiciona o repositório à sua lista
echo "deb https://download.opensuse.org/repositories/home:/k8sgpt-ai:/stable/xUbuntu_22.04/ /" | sudo tee /etc/apt/sources.list.d/k8sgpt.list

# Instala o K8sGPT
sudo apt update
sudo apt install k8sgpt
\`\`\`

### 2. Configuração do Backend de IA (OpenAI)
\`\`\`bash
# Você precisará de uma chave de API da OpenAI (platform.openai.com)
k8sgpt auth add
\`\`\`
Siga as instruções para selecionar \`openai\` como backend e cole sua chave de API.

## 🚀 Cenário de Treino Prático: \`ImagePullBackOff\`

Vamos usar a metodologia na prática.

### 1. Crie um Pod com erro:
\`\`\`bash
# Aplique o manifesto com o nome da imagem incorreto
kubectl apply -f examples/pod-errado.yaml
\`\`\`

### 2. Diagnóstico Manual (Seu Treino CKA):
\`\`\`bash
# Verifique o status do Pod
kubectl get pods

# Investigue os eventos para encontrar a causa-raiz
kubectl describe pod pod-com-erro
\`\`\`

### 3. Validação com o "Professor" K8sGPT:
\`\`\`bash
# Peça a análise e a explicação
k8sgpt analyze --explain
\`\`\`
Compare a saída do K8sGPT com a sua própria conclusão. Essa validação acelera o aprendizado e aprofunda o entendimento.
EOF
