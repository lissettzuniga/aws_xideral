# aws_xideral

# Tarea No.1 documentación.

## 1. Instalar WSL2 y Ubuntu

Abrir PowerShell como administrador y ejecutar:

wsl --install

Reiniciar Windows cuando sea solicitado. Después, verificar que Ubuntu utilice WSL2:

wsl --list --verbose

Iniciar Ubuntu:

wsl -d Ubuntu

Desde este punto, los comandos se ejecutan en Bash dentro de Ubuntu.

cd ~
echo $SHELL

El shell debe ser /bin/bash.

## 2. Actualizar Ubuntu

sudo apt update
sudo apt upgrade -y

## 3. Configurar Docker

Después de instalar Docker Desktop y habilitar la integración con Ubuntu en WSL2, validar desde Bash:

docker --version

Crear el grupo docker y agregar el usuario actual:

sudo groupadd -f docker
sudo usermod -aG docker $USER

Cerrar y volver a abrir Ubuntu para aplicar el cambio. Después, ejecutar:

groups
docker run hello-world

La instalación es correcta cuando aparece Hello from Docker!.

## 4. Instalar las dependencias de Python

sudo apt install -y \
  make \
  build-essential \
  libssl-dev \
  zlib1g-dev \
  libbz2-dev \
  libreadline-dev \
  libsqlite3-dev \
  curl \
  git \
  llvm \
  libncurses-dev \
  xz-utils \
  tk-dev \
  libxml2-dev \
  libxmlsec1-dev \
  libffi-dev \
  liblzma-dev

## 5. Instalar pyenv

Clonar el proyecto:

git clone https://github.com/pyenv/pyenv.git ~/.pyenv

Comprobar la descarga:

ls ~/.pyenv

Configurar pyenv para Bash:

echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init - bash)"' >> ~/.bashrc
source ~/.bashrc

Verificar:

pyenv --version

## 6. Instalar Python 3.14.7

pyenv install --list | grep " 3.14"
pyenv install 3.14.7
pyenv versions
pyenv global 3.14.7
pyenv rehash
python --version

El resultado esperado es:

Python 3.14.7

## 7. Crear el workspace y el entorno virtual

mkdir -p ~/jupyter
cd ~/jupyter
python --version
python -m venv .venv
source .venv/bin/activate

El prefijo (.venv) confirma que el entorno virtual está activo.

## 8. Instalar y ejecutar Jupyter Notebook.
<img width="1198" height="642" alt="image" src="https://github.com/user-attachments/assets/cd14cc9f-7bfe-46c5-979e-822e557374ee" />
