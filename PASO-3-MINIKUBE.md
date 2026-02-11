# Paso 3: Instalación de Minikube en WSL Debian

**Fecha:** $(date +%Y-%m-%d)
**Contexto:** Tutorial para levantar Kubernetes local con driver Docker.

## 📦 Instalación
\`\`\`bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
rm minikube-linux-amd64
minikube version
\`\`\`

## 🛠️ Fix para WSL2 (cgroups)
\`\`\`bash
sudo mkdir -p /sys/fs/cgroup/systemd
sudo mount -t cgroup -o none,name=systemd cgroup /sys/fs/cgroup/systemd
\`\`\`
*Nota: Este comando se pierde al reiniciar. Para hacerlo permanente:*
\`\`\`bash
echo 'sudo mkdir -p /sys/fs/cgroup/systemd && sudo mount -t cgroup -o none,name=systemd cgroup /sys/fs/cgroup/systemd' >> ~/.bashrc
\`\`\`

## ⚙️ Configuración y Arranque
\`\`\`bash
minikube config set driver docker
minikube start --cpus 2 --memory 4096
\`\`\`

## 🔧 Instalación de kubectl
\`\`\`bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
rm kubectl
kubectl version --client
\`\`\`

## ✅ Verificación
\`\`\`bash
minikube status
kubectl get nodes
kubectl get pods -A
\`\`\`

## 🎛️ Addons activados
\`\`\`bash
minikube addons enable dashboard
minikube addons enable ingress
minikube dashboard --url
\`\`\`
