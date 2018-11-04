# dev-pec2.2 - Módulo 3 Diseño y desarrollo

## EJERCICIO 3

**SWARM** 

---

**1. Instalar swarm**

Seguir las instrucciones en [https://swarm-guide.readthedocs.io/en/latest/installation.html](https://swarm-guide.readthedocs.io/en/latest/installation.html)

```
sudo apt-get install software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install ethereum-swarm
```

![01.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio3/01.png "01")

---

**2. Crear una cuenta y arrancar un nodo swarm**

Seguir las instrucciones en [https://swarm-guide.readthedocs.io/en/latest/gettingstarted.html](https://swarm-guide.readthedocs.io/en/latest/gettingstarted.html)

Crear una cuenta con

`geth account new`.

El resultado fue nuestra cuenta:

`9b4c0b74f50c12a018d7c0af9c23083b20473a1d`

(usaremos el resultado de este comando en el siguiente paso)

Conectar con swarm con `swarm --bzzaccount <your-account-here>`

En nuestro caso `swarm --bzzaccount 9b4c0b74f50c12a018d7c0af9c23083b20473a1d`

![02.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio3/02.png "02")

---

**3. Verificar que el nodo esta corriendo**

Apunto mi navegador web hacia [http://localhost:8500/](http://localhost:8500/) veo que efectivamente aparece la pagina que un nodo de swarm sirve por defecto.

![03.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio3/03.png "03")

---

**4. Conectar con rinkeby**

En un terminal aparte, abrimos geth para que sincronice con rinkeby.

`geth --rinkeby`

NOTA: esto puede tardar un par de dias en estar completamente sincronizado. En nuestro caso ya lo tenemos sincronizado despues de haberlo dejado sincronizando durante un par de dias para hacer el ejercicio 1.

OBSERVACION: (alternativa) para conectar con swarm es suficiente con estar conectado a rinkeby aunque no se tengan todos los bloques sincronizados. Esto puede conseguirse lanzando `geth --rinkeby --syncmode=light`

![04.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio3/04.png "04")

---

**5. Hacer que el nodo corra resolviendo ENS en rinkeby**

Detenemos la instruccion que lanzamos en el punto 3 (`swarm --bzzaccount <your-account-here>`) y en su lugar lanzamos esta:

`swarm --ens-api '$HOME/.ethereum/rinkeby/geth.ipc' --bzzaccount <your-account-here>`

en nuestro caso

`swarm --ens-api '$HOME/.ethereum/rinkeby/geth.ipc' --bzzaccount 9b4c0b74f50c12a018d7c0af9c23083b20473a1d`

![05.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio3/05.png "05")

---

**6. Subir a swarm nuestra carpeta dist**

Crear carpeta dist con lo que queremos subir a swarm (ver en el [ejercicio 2](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio2) el punto "6. Crear directorio *dist* con lo que queremos publicar").

Subimos a swarm nuestros ficheros con la siguiente instruccion:

`swarm --recursive up <directory-name>`

En nuestro caso:

`swarm --recursive up dist`

![06.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio3/06.png "06")
