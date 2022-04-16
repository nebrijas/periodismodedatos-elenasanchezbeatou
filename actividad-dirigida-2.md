# Actividad Dirigida 2

## Importar librerías

Importo la librería [requests](https://docs.python-requests.org/en/latest/). Esta librería nos permite realiazar peticiones HTTP.

Voy a importar de la librería [bs4](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) `BeautifulSoup` . Esta librería nos permite poder recabar información de un código HTML.

## Variables

Una variable hace referencia a un objeto cualquiera. Este objeto puede ser un int, string u otro tipo de objeto.

### Definimos URL

Asignamos a la variable URL el string correspondiente con el enlace deseado.

### Realizamos la petición a la web

Realizamos una petición a la URL indicada y la asignamos a la variable req.

Si el código de respuesta HTTP es distinto de 200 significa que ha ocurrido un error en la peticion HTTP.

### De requests a BeautifulSoup

Pasamos el contenido HTML de la web a un objeto `BeautifulSoup()`. Esta libreria nos permite obtener información del codigo HTML.

### Variables de datos

Definimos las variables `paises`, `oros`, etc (para asociar la informacion a las variables en el codigo) y las identificamos con la función `find_all()`

## Hacemos la pregunta

Preguntamos al usuario mediante la función input si quiere saber los 20 paises con mas medallas. Se guarda su respuesta en la variable respuesta. Si esta es igual a 's' entonces lanza el mensaje 'Vale, vamos a ello'.

## Bucle para obtener los datos

Recorremos los distintos arrays obtenidos gracias a `find_all()` para así poder mostrar por pantalla los 20 primeros paises del medallero.

## Código Bruto:

```
from bs4 import BeautifulSoup
import requests
#Datos sobre los Juegos Olímpicos en 2020

respuesta=input('¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?\n \n Si tu respuesta es Sí, presiona "s" \n')
if(respuesta == 's'):
  print('\nRESULTADOS DE LOS DATOS DE LOS JUEGOS OLÍMPICOS 2020\n')
  print ('PAÍSES')
  URL = "https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/"
  # Realizamos la petición a la web
  req = requests.get(URL)
  # Si el estatus code no es 200 no se puede leer la página
  if (req.status_code != 200):
    raise Exception("No se puede hacer Web Scraping en"+ URL)
  # Pasamos el contenido HTML de la web a un objeto BeautifulSoup()
  html = BeautifulSoup(req.text, "html.parser")
  # Obtenemos todos los divs donde están las entradas
  paises = html.find_all("th",{"class":"pais"})
  oros = html.find_all("td",{"class":"m_oro"})
  platas = html.find_all("td",{"class":"m_plata"})
  bronces = html.find_all("td",{"class":"m_bronce"})
  totales = html.find_all("td",{"class":"m_total"})
  for i in range (20):
    # Con el método "getText()" no nos devuelve el HTML
    print("%d. %s \nOro: %s Plata: %s Bronce: %s \n Total: %s \n " % (i+1, paises[i+1].text.strip(),oros[i].text.strip(),platas[i].text.strip(),bronces[i].text.strip(), totales[i].text.strip()))

else:
  print('Qué lástima, y...')
```
