# Introducción
En esta guia te ayudare a configurar Flet para crear un apk y ejecutable en Linux (Debian 12 y derivadas), con la ayuda de Android Studio y Flutter SDK
Por favor lea los prerrequisitos y siga los paso a continuación

# Antes de empezar
En Debian si aun no lo has hecho edita el archivo 'sudoers' para otorgarte privilegios de sudo
  
1. Accede como root
```bash
su -
```

2. Edita el archivo sudoers usando visudo
```bash
visudo
```

3. Esto abrirá el archivo /etc/sudoers en un editor de texto. Añade la siguiente línea al final del archivo (cambiar segun su nombre de usuario)
```bash
nombre_usuario ALL=(ALL:ALL) ALL
```

# Prerrequisitos
Aquí les presento un resumen de los prerrequisitos según [Android Studio](https://developer.android.com/studio/install?hl=es-419#64bit-libs) y [Flutter SDK](https://docs.flutter.dev/get-started/install/linux/desktop#development-tools):
```bash
sudo apt update && sudo apt upgrade -y
```
```bash
sudo apt install -y curl git unzip xz-utils zip libglu1-mesa python3-venv
```
```bash
sudo apt install -y clang cmake ninja-build pkg-config libgtk-3-dev liblzma-dev libstdc++-12-dev
```

# 1. Instalar Android Studio
- Ir a esta pagina y descargar Android Studio: https://developer.android.com/studio
- Ir a la carpeta de descarga:
```bash
cd Descargas
```
- Descomprimir el archivo descargado y copiarlo a ```/usr/local/```
```bash
sudo tar -xf android-studio-2024.1.1.12-linux.tar.gz -C /usr/local/
```
- Ir a la siguente ruta
```bash
cd /usr/local/android-studio/bin
```
- Ejecutar Android Studio, escojer instalación estandar, aceptar los terminos y condiciones e instalar los SDK
```bash
./studio.sh
```
- Una vez finalizado la instalación cerrar Android Studio

# 2. Instalar Flutter SDK
- Ir a esta pagina, escojer 'descargar e instalar' y descargar Flutter SDK: https://docs.flutter.dev/get-started/install/linux/desktop#install-the-flutter-sdk
- Ir a la carpeta de descarga:
```bash
cd Descargas
```
- Descomprimir el archivo descargado y copiarlo a ```/usr/local/```
```bash
sudo tar -xf flutter_linux_3.24.0-stable.tar.xz -C /usr/local/
```
- Agregar Flutter SDK al PATH
```bash
echo 'export PATH="$PATH:/usr/local/flutter/bin"' >> ~/.bashrc
```
- Actualizar el PATH
```bash
source ~/.bashrc
```
- Verificar si Flutter SDK funciona correctamente:
```bash
flutter doctor
```
- Te deberia salir algo parecido a esto:
```bash
Doctor summary (to see all details, run flutter doctor -v):
[✓] Flutter (Channel stable, 3.24.0, on Debian GNU/Linux 12 (bookworm)
    6.1.0-23-amd64, locale es_EC.UTF-8)
[!] Android toolchain - develop for Android devices (Android SDK version 35.0.0)
    ✗ cmdline-tools component is missing
      Run `path/to/sdkmanager --install "cmdline-tools;latest"`
      See https://developer.android.com/studio/command-line for more details.
    ✗ Android license status unknown.
      Run `flutter doctor --android-licenses` to accept the SDK licenses.
      See https://flutter.dev/to/linux-android-setup for more details.
[✗] Chrome - develop for the web (Cannot find Chrome executable at
    google-chrome)
    ! Cannot find Chrome. Try setting CHROME_EXECUTABLE to a Chrome executable.
[✓] Linux toolchain - develop for Linux desktop
[✓] Android Studio (version 2024.1)
[✓] Connected device (1 available)
[✓] Network resources

! Doctor found issues in 2 categories.
```

# 3. Instalar Flet
- Crea o ve a donde quieras tener tu proyecto
```bash
mkdir Documentos/mi-proyecto
cd Documentos/mi-proyecto
```
- Crear un entorno virtual Python en una carpeta de su preferencia
```bash
python3 -m venv .venv
```
- Activar el entorno virtual
```bash
source .venv/bin/activate
```
- Instalar Flet con pip
```bash
pip install flet
```
- Crear un proyecto Flet (cambia 'ejemplo' por el nombre que quiera para tu proyecto)
```bash
flet create ejemplo
```
- Entrar en el proyecto
```bash
cd ejemplo
```
# 4. Crear APK y ejecutable para Linux
- Crea APK
```bash
flet build apk
```
- Crea APK para arm64-v8a:
```bash
flet build apk --flutter-build-args=--target-platform --flutter-build-args=android-arm64
```
- Crea APK para armeabi-v7a:
```bash
flet build apk --flutter-build-args=--target-platform --flutter-build-args=android-arm
```
- Crear ejecutable Linux
```bash
flet build linux
```
