# dev-pec2.2 - Módulo 3 Diseño y desarrollo

## EJERCICIO 2

**IPFS** 

---

**1. Hacer pequeña modificación en proyecto pet-shop**

He cambiado `Pete` por `Ana` en el fichero `index.html`.

![01.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio2/01.png "01.png")

---

**2. Subir proyecto pet-shop modificado a github (sin incluir node_modules)**

Para que la carpeta `node_modules` no se incluya, en la raiz del proyecto pet-shop incluyo el fichero `.gitignore` con la linea `node_modules`.

```
git add index.html
git commit "Little changes in index.html (show my name)"
git push -u origin master
```

![02.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio2/02.png "02.png")

---

**3. Instalar IPFS**

Descargar el binario de [https://dist.ipfs.io/#go-ipfs](https://dist.ipfs.io/#go-ipfs)

Seguir las instrucciones de instalación de [https://docs.ipfs.io/introduction/install](https://docs.ipfs.io/introduction/install)

```
cd ~/Descargas
tar xvfz go-ipfs_v0.4.17_linux-amd64.tar.gz
cd go-ipfs
sudo ./install.sh
```

![03.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio2/03.png "03.png")

---

**4. Inicializar el repositorio de IPFS**

Una vez instalado IPFS, inicializamos el repositorio IPFS con la siguiente instruccion:

`ipfs init`

Cuyo resultado es:

```
initializing ipfs node at /home/ana/.ipfs
generating 2048-bit RSA keypair...done
peer identity: QmVxzwryaUcNPhmA6y6PKCia7752j3p1gcpA3t29XztELp
to get started, enter:

  ipfs cat /ipfs/QmS4ustL54uo8FzR9455qaxZwuMiUhyvMcX9Ba8nUH4uVv/readme
```

---

**5. Iniciar IPFS daemon**

`ipfs daemon`

![05.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio2/05.png "05")

---

**6. Crear directorio *dist* con lo que queremos publicar**

Observamos el contenido del fichero `bs-config.json`.

```
{
  "server": {
    "baseDir": ["./src", "./build/contracts"]
  }
}
```

Esto indica a `lite-server` (servidor web local utilizado para hacer el despliegue en local) que directorios tiene que servir, es decir el directorio `./src` y `./build/contracts` del proyecto truffle.

Creamos el directorio `dist` en nuestro proyecto truffle y copiamos el contenido de dichos directorios en él.

```
cd  ~/git/dev-pec2.2.2/ejercicio2/pet-shop-tutorial
mkdir dist
cp -dpRv src dist
cp -dpRv build/contracts dist
```

---

**7. Añadir el directorio dist a IPFS**

Añadimos el directorio `dist` a IPFS.

`ipfs add -r -w dist`

El flag -r (--recursive) hace que se añada el directorio recursivamente (con los subdirectorios que contenga)

El flag -w (--wrap-with-directory) hace que cada archivo se añada como un objeto con la referencia del cual es el directorio al que pertenece.

En este caso, es importante usar el flag -w por que en el archivo dist/src/js/app.js hay una referencia a ../pets.json que no funcionaria correctamente si no se usara dicho flag.

Lo importante de la respuesta es el hash asociado al directorio `dist` (que usaremos en el siguiente paso)

`added QmZMQPGgUesS2RmPqPRgd9SJ5h7TATqCTEKtdCZYMyTAdx dist`

![07.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio2/07.png "07")

---

**8. Publicar el recurso añadido a IPFS**

Hacemos disponible al publico el recurso añadido.

`ipfs name publish QmZMQPGgUesS2RmPqPRgd9SJ5h7TATqCTEKtdCZYMyTAdx`

Respuesta:

`Published to QmVxzwryaUcNPhmA6y6PKCia7752j3p1gcpA3t29XztELp: /ipfs/QmZMQPGgUesS2RmPqPRgd9SJ5h7TATqCTEKtdCZYMyTAdx`

![08.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio2/08.png "08")

---

**9. Comprobamos que nuestra Dapp esta publicamente disponible**

Apuntamos nuestro navegador a:

[https://gateway.ipfs.io/ipfs/QmZMQPGgUesS2RmPqPRgd9SJ5h7TATqCTEKtdCZYMyTAdx/](https://gateway.ipfs.io/ipfs/QmZMQPGgUesS2RmPqPRgd9SJ5h7TATqCTEKtdCZYMyTAdx/)

![09.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio2/09.png "09")

Transacción con metamask:

![10.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio2/10.png "10")

Transacciones minadas:

![11.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio2/11.png "11")

Operaciones confirmadas:

![12.png](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio2/12.png "12")

---
