# 🔒 Chat Seguro Multiusuario (Python + SSL/TLS)

Una aplicación de chat cliente-servidor implementada en Python que utiliza **Sockets** para la comunicación y **SSL/TLS, RSA, AES-256** para cifrar los mensajes, garantizando la privacidad de la conversación. Incluye una interfaz gráfica (GUI) construida con **Tkinter**.

## Características

* **Comunicación Encriptada:** Todo el tráfico entre el cliente y el servidor está protegido mediante SSL (Secure Sockets Layer).
* **Arquitectura Cliente-Servidor:** Soporte para múltiples clientes conectados simultáneamente gracias al uso de `threading`.
* **Interfaz Gráfica:** Cliente amigable construido con Tkinter.
* **Comandos de Chat:** Funcionalidades como listar usuarios conectados.
* **Notificaciones:** Avisos de conexión y desconexión de usuarios en tiempo real.

## Requisitos Previa

* **Python 3.10+** (Recomendado).
* **OpenSSL** (Para generar los certificados de seguridad).
* Librería `tkinter` (Generalmente incluida en Python, en Linux puede requerir `sudo apt-get install python3-tk`).

## Instalación y Configuración

Sigue estos pasos para poner en marcha el proyecto en tu máquina local.

### 1. Clonar el repositorio

```bash
git clone [https://github.com/TU-USUARIO/TU-REPOSITORIO.git](https://github.com/TU-USUARIO/TU-REPOSITORIO.git)
cd TU-REPOSITORIO
```
### 2. Generar Certificados SSL (Importante)

Para que el servidor seguro funcione, necesitas generar un certificado autofirmado y una clave privada. Los archivos `.key` y `.pem` **no se incluyen en el repositorio por seguridad**.

Ejecuta los siguientes comandos en tu terminal (dentro de la carpeta del proyecto):

```bash
# 1. Generar la clave privada (pedirá una contraseña temporal)
openssl genpkey -algorithm RSA -out server-key.key -aes256

# 2. Generar la solicitud de firma de certificado (CSR)
openssl req -new -key server-key.key -out server.csr

# 3. Generar el certificado autofirmado (valido por 365 días)
openssl x509 -req -days 365 -in server.csr -signkey server-key.key -out server-cert.pem

# 4. Eliminar la contraseña de la clave privada (CRUCIAL para que el script de Python corra sin interrupciones)
openssl rsa -in server-key.key -out server-key.key
```

## ▶️ Uso

### 1. Iniciar el Servidor
Primero debes iniciar el servidor, que esperará las conexiones entrantes.

```bash
python3 server.py
```
### 1. Iniciar el Cliente
Abre una nueva terminal (o varias) para simular diferentes usuarios.
```bash
python3 client.py
```

## Nota sobre Seguridad

Este proyecto utiliza certificados autofirmados.
- Servidor: Está configurado para cargar el certificado local.
- Cliente: Está configurado para CERT_NONE (no verificar la autoridad del certificado) para facilitar las pruebas en entornos locales (localhost). En un entorno de producción real, se debería utilizar un certificado emitido por una CA (Autoridad Certificadora) válida y activar la verificación en el cliente.
