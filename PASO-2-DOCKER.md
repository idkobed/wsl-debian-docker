# Paso 2: Instalación de Docker en Debian (WSL)

En este paso se instala **Docker Engine** en Debian ejecutándose sobre **WSL**, se configuran los permisos correctos y se valida que Docker funcione correctamente.

---

## 🎯 Objetivo del paso

* Instalar Docker desde el repositorio oficial
* Configurar Docker para usarse sin `sudo`
* Verificar la instalación con un contenedor de prueba

---

## 1️⃣ Actualizar el sistema

Antes de instalar Docker, actualizamos los paquetes del sistema:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 2️⃣ Instalar dependencias necesarias

Docker necesita algunas herramientas básicas para funcionar correctamente:

```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```

---

## 3️⃣ Agregar la clave GPG oficial de Docker

Esto permite que Debian confíe en los paquetes descargados desde Docker:

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

---

## 4️⃣ Agregar el repositorio oficial de Docker

Se indica a Debian desde dónde obtener Docker:

```bash
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/debian \
$(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Actualizamos nuevamente los repositorios:

```bash
sudo apt update
```

---

## 5️⃣ Instalar Docker Engine

Instalamos Docker y sus componentes principales:

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

---

## 6️⃣ Configurar permisos para usar Docker sin sudo

Agregamos el usuario actual al grupo `docker`:

```bash
sudo usermod -aG docker $USER
```

> ⚠️ Es obligatorio cerrar y volver a abrir la terminal para que los permisos se apliquen.

---

## 7️⃣ Verificar la instalación

Ejecutamos el contenedor de prueba:

```bash
docker run hello-world
```

### Resultado esperado

```text
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

---

## ✅ Conclusión

Docker quedó instalado y funcionando correctamente en Debian bajo WSL. El sistema está listo para continuar con Docker Compose y Kubernetes (Minikube).

---

➡️ **Siguiente paso:** Instalación de Minikube en WSL
