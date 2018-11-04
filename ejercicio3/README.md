# dev-pec2 - Módulo 3 Diseño y desarrollo

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

![pantalla-ej3-01.png](https://github.com/anakb/dev-pec2/blob/master/ejercicio-3/1.png "pantalla-ej3-01")
---

**2. Arrancar un nodo swarm**

Seguir las instrucciones en [https://swarm-guide.readthedocs.io/en/latest/gettingstarted.html](https://swarm-guide.readthedocs.io/en/latest/gettingstarted.html)

Creo una cuenta con `geth account new`. Usare el resultado de este comando en el siguiente.

Conecto con swarm con `swarm --bzzaccount <your-account-here>`

![pantalla-ej3-02.png](https://github.com/anakb/dev-pec2/blob/master/ejercicio-3/2.png "pantalla-ej3-02")
---

**3. Verificar que el nodo esta corriendo**

Apunto mi navegador web hacia [http://localhost:8500/](http://localhost:8500/) veo que efectivamente aparece la pagina que un nodo de swarm sirve por defecto.

![pantalla-ej3-03.png](https://github.com/anakb/dev-pec2/blob/master/ejercicio-3/3.png "pantalla-ej3-03")
---
