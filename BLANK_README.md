"""
    Este programa reconoce la voz mediante microfono y transcribe
    de audio a texto desde el momento en que se inicializa el mismo.
    Tiene varias funciones definidas, las cuales se ejecutan
    si se reconoce una palabra clave, como por ej (reproducir).
"""

import pyttsx3
import speech_recognition as sr
import pywhatkit
import yfinance as yf
import pyjokes
import webbrowser
import datetime
import wikipedia

# tomar el audio y transformarlo en texto
def trans_audio_texto():

    # almacernar recognizer en variable
    r = sr.Recognizer()

    # configurar el microfono
    with sr.Microphone() as origen:

        # tiempo de espera
        r.pause_threshold = 0.8

        # arranca la grabacion
        print("ya puedes hablar")

        # guardar el audio
        audio = r.listen(origen)

        try:
            # buscar en google
            pedido = r.recognize_google(audio, language="es-ar")

            # prueba de que se grabo
            print ("dijiste: " + pedido)

            return  pedido

        # en caso de error
        except sr.UnknownValueError:

            # prueba de que no grabo el audio
            print ("ups, no entendi")

            # devolver error
            return  "sigo esperando"

        # en caso de no resolver el pedido
        except sr.RequestError:

            # prueba de que no grabo el audio
            print("ups, error de servicio")

            # devolver error
            return "sigo esperando"

        # error inesperado
        except:

            # prueba de que no grabo el audio
            print("ups, hubo un error")

            # devolver error
            return "sigo esperando"


# funcion para que el asistente pueda ser escuchando
def hablar(mensaje):

    # enceder el motor de pyttsx3
    engine = pyttsx3.init()

    # pronunciar mensaje
    engine.say(mensaje)
    engine.runAndWait()


# informar dia de la semana
def pedir_dia():

    # crear variable con dia de la fecha
    dia = datetime.date.today()

    # crear variable para el dia de semana
    dia_semana = dia.weekday()

    # diccionario con nombre de dias
    calendario = {0: 'Lunes',
                  1: 'Martes',
                  2: 'Miércoles',
                  3: 'Jueves',
                  4: 'Viernes',
                  5: 'Sábado',
                  6: 'Domingo'}

    # decir el dia e la semana
    hablar(f'Hoy es {calendario[dia_semana]}')


# informar hora
def pedir_hora():

    # crear una variable con datos de la hora
    hora = datetime.datetime.now()
    hora = f'en este momento son las {hora.hour} con {hora.minute} minutos'

    # decir la hora
    hablar(hora)


# funcion saludo inicial
def saludo():

    # crear variable de momento horario
    hora = datetime.datetime.now()
    if hora.hour < 6 or hora.hour > 20:
        momento = 'Buenas noches'
    elif 6 <= hora.hour < 13:
        momento = 'Buen dia'
    else:
        momento = 'Buenas tardes'



    # saludar
    hablar(f'{momento}, soy Daeneris Targarien, madre de '
           'dragones e hija de la tormenta. Por favor, dime tu nombre')


# funcion central del asistente
def pedir_cosas():

    # activar saludo
    saludo()

    # variable de corte
    comenzar = True

    while comenzar:

        # activar microfono y guardar grabacion
        pedido = trans_audio_texto().lower()

        if 'abrir youtube' in pedido:
            hablar('Con gusto, abrire youtube')
            webbrowser.open('https://www.youtube.com')
            continue
        elif 'abrir navegador' in pedido:
            hablar('abriendo el navegador')
            webbrowser.open('https://google.com')
            continue
        elif 'qué día es hoy' in pedido:
            pedir_dia()
            continue
        elif 'qué hora es' in pedido:
            pedir_hora()
            continue
        elif 'reproducir' in pedido:
            hablar('vamos a escucharlo')
            pywhatkit.playonyt(pedido)
        elif 'adiós' in pedido:
            hablar('Entendido, me ire a dormir, adios')
            break

pedir_cosas()
