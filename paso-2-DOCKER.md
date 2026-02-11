# Paso 2: Instalación de Docker en Debian (WSL)

En este paso instalaremos Docker dentro de Debian ejecutándose en WSL.

---

## 1. Actualizar el sistema

```bash
sudo apt update && sudo apt upgrade -y

---------------

## 2. Instalar dependencias necesarias
sudo apt install -y ca-certificates curl gnupg lsb-release

---------------

## 3.Añadir la clave GPG oficial de Docker
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

---------------

## 4. Agregar el repositorio de Docker
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/debian \
$(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

----------------

## 5. Instalar Docker
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io

----------------

## 6. Permitir usar Docker sin sudo
sudo usermod -aG docker $USER

----------------

## 7. Verificar instalación
docker run hello-world

-----------------

## 8. resultado esperado
Hello from Docker!
This message shows that your installation appears to be working correctly.


-DOCKER INSTALADO CORRECTAMENTE-
