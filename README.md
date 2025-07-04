# Documentación del Asistente por Voz en Python

**Versión:** 1.0  
**Autor:** Mauricio Basaure  
**Fecha:** 04/07/2025

---

## 🧾 Resumen

Este programa permite controlar funciones básicas mediante comandos de voz en español, incluyendo abrir sitios web, decir la hora, reproducir videos, entre otras funcionalidades. Utiliza reconocimiento de voz, síntesis de voz y APIs de terceros.

---

## ⚙️ Requisitos del Sistema

- Python 3.x  
- Sistema operativo: Windows (probado en Windows 10)  
- Micrófono funcional  
- Librerías necesarias:
  - `pyttsx3`
  - `speech_recognition`
  - `pywhatkit`
  - `yfinance`
  - `pyjokes`
  - `wikipedia`

---

## 🔧 Instalación y Ejecución

```bash
# 1. Crear entorno virtual
python -m venv venv

# 2. Activar entorno (Windows)
venv\Scripts\activate

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Ejecutar el programa
python main.py
```

---

## 🧠 Estructura del Programa

- **`trans_audio_texto()`**: Convierte audio capturado por micrófono en texto usando reconocimiento de voz.  
- **`hablar(mensaje)`**: Sintetiza y reproduce mensajes hablados.  
- **`pedir_dia()`**: Informa el día actual.  
- **`pedir_hora()`**: Informa la hora actual.  
- **`saludo()`**: Saludo personalizado según la hora del día.  
- **`pedir_cosas()`**: Función central que escucha continuamente y responde comandos por voz.

---

## 🎙️ Comandos de Voz Soportados

- `"abrir youtube"`  
- `"abrir navegador"`  
- `"qué día es hoy"`  
- `"qué hora es"`  
- `"reproducir [nombre de video o canción]"`  
- `"adiós"`

---

## 🛠️ Errores Comunes y Soluciones

- **Error:** `No module named 'pyaudio'`  
  **Solución:** Ejecutar `pip install pipwin` y luego `pipwin install pyaudio`

- **Problema:** El micrófono no funciona  
  **Solución:** Verificar permisos del sistema o drivers de audio

- **Error:** `speech_recognition.RequestError`  
  **Solución:** Comprobar la conexión a Internet

---

## 🚀 Posibilidades de Mejora

- Incluir comandos personalizados según el usuario  
- Guardar historial de interacciones  
- Añadir integración con otras plataformas (Telegram, WhatsApp, etc.)  
- Responder preguntas frecuentes con inteligencia artificial
