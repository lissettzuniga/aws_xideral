# aws_xideral
Tarea 1: Preparación del entorno de desarrollo

Alumna: Lissett Zúñiga Reyes
Entorno: Windows, WSL2, Ubuntu, Bash, Docker, Python y Jupyter Notebook

Objetivo

Preparar un entorno local de desarrollo en Windows utilizando Ubuntu sobre WSL2. El entorno incluye Bash, Docker, Python 3.14.7 administrado con pyenv, un ambiente virtual de Python y Jupyter Notebook.

1. Instalación de WSL2 y Ubuntu

Abrí PowerShell como administrador y ejecuté:

wsl --install

Después reinicié Windows y comprobé que Ubuntu estuviera utilizando WSL2:

wsl --list --verbose

El valor de la columna VERSION debe ser 2.

Para iniciar Ubuntu desde PowerShell utilicé:

wsl -d Ubuntu

Ya dentro de Ubuntu, verifiqué el sistema, usuario, directorio y shell:

uname -a
whoami
cd ~
pwd
echo $SHELL

El comando echo $SHELL debe mostrar /bin/bash.



2. Actualización de Ubuntu

Actualicé la información de los paquetes y las aplicaciones instaladas:

sudo apt update
sudo apt upgrade -y

3. Instalación y configuración de Docker

Instalé Docker Desktop para Windows y habilité su integración con WSL2 desde:

Docker Desktop → Settings → General → Use the WSL 2 based engine
Docker Desktop → Settings → Resources → WSL Integration → Ubuntu

Después comprobé la instalación desde Bash:

docker --version

Agregué mi usuario al grupo docker para ejecutar Docker sin sudo:

sudo groupadd -f docker
sudo usermod -aG docker $USER

Cerré la sesión de Ubuntu y volví a abrirla para aplicar el cambio. Luego validé el grupo y ejecuté el contenedor de prueba:

groups
docker run hello-world

La instalación es correcta cuando aparece el mensaje Hello from Docker!.



4. Instalación de dependencias para Python

Instalé las herramientas y bibliotecas necesarias para compilar Python:

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

5. Instalación y configuración de pyenv

Cloné el repositorio de pyenv dentro de mi carpeta personal:

git clone https://github.com/pyenv/pyenv.git ~/.pyenv

Comprobé su contenido:

ls ~/.pyenv

Como el shell utilizado es Bash, agregué la configuración a ~/.bashrc:

echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init - bash)"' >> ~/.bashrc
source ~/.bashrc

Verifiqué la instalación:

pyenv --version

6. Instalación de Python 3.14.7

Consulté las versiones disponibles de Python 3.14:

pyenv install --list | grep " 3.14"

Instalé y seleccioné Python 3.14.7:

pyenv install 3.14.7
pyenv versions
pyenv global 3.14.7
pyenv rehash

Validé la versión y el ejecutable:

python --version
which python

El resultado esperado de la versión es:

Python 3.14.7



7. Creación del workspace y entorno virtual

Creé el directorio de trabajo para Jupyter:

mkdir -p ~/jupyter
cd ~/jupyter

Creé y activé un entorno virtual:

python -m venv .venv
source .venv/bin/activate

Cuando el entorno está activo, el prompt comienza con (.venv).

Actualicé pip e instalé Jupyter Notebook y el kernel de Python:

python -m pip install --upgrade pip
pip install notebook
pip install ipykernel

8. Ejecución de Jupyter Notebook

Con el entorno virtual activo, inicié Jupyter:

jupyter notebook

En un notebook ejecuté el siguiente código para comprobar la versión de Python y la ruta del entorno virtual:

import sys

print("Python version:")
print(sys.version)

print("\nPython executable:")
print(sys.executable)

El ejecutable utilizado debe encontrarse dentro de:

/home/lissett/jupyter/.venv/bin/python



9. Apertura automática de Jupyter en Windows

Para que WSL abra el navegador predeterminado de Windows, creé el archivo ~/bin/wsl-browser:

#!/bin/bash
/mnt/c/Windows/System32/cmd.exe /c start "" "$1"

Le asigné permiso de ejecución y lo configuré como navegador de Bash:

chmod +x ~/bin/wsl-browser
echo 'export BROWSER="$HOME/bin/wsl-browser"' >> ~/.bashrc
source ~/.bashrc

También deshabilité el archivo de redirección de Jupyter, ya que Windows no puede abrir directamente una ruta file:/home/... de Linux:

mkdir -p ~/.jupyter
echo 'c.ServerApp.use_redirect_file = False' >> ~/.jupyter/jupyter_server_config.py

Finalmente, para iniciar una nueva sesión:

cd ~/jupyter
source .venv/bin/activate
jupyter notebook

Resultado

El entorno local quedó configurado correctamente con:

Ubuntu ejecutándose sobre WSL2.

Bash como shell.

Docker funcionando sin sudo.

Python 3.14.7 administrado con pyenv.

Entorno virtual aislado en .venv.

Jupyter Notebook ejecutándose en el navegador de Windows.
