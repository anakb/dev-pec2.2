# dev-pec2 - Módulo 3 Diseño y desarrollo

## EJERCICIO 1

**Adquiera un dominio bajo el TLD ‘.test’ en la testnet que desee (Rinkeby o Ropsten).  Si   no   le   es   posible   sincronizar   un   nodo,   puede   desplegar   el   servicio   ENS   en   la   red   testrpc con Geth. Describa el procedimiento seguido. Demuestre   que   es   usted   poseedor   del   dominio   adquirido   y   obtenga   la   dirección   del  Resolver utilizado** 

---

Para sincronizar el nodo con Rinkeby he utilizado el cliente de Geth: 

`geth --rinkeby`

La sincronización tardó un par de días. 

Mientras inicializaba la sincronización me bajé del repositorio de ENS en GIT HUB (ens-master.zip). Del repositorio copié el archivo ensutils-testnet.js donde realicé los siguientes cambios para trabajar en Rinkeby:

`contract address: 0xe7410170f87102df0055eb195163a03b7f2bff4a (line 220)`
`publicResolver address: 0x5d20cf83cb385e06d2f2a892f9322cd4933eacdc (line 1314)`

Una vez hechos los cambios en las líneas del archivo ensutils-testnet.js. Empecé a usar la consola de Ethereum con las siguientes instrucciones:

`Rinkeby: geth --rinkeby attach`

`eth.accounts` 

Mi cuenta con ETH es 0xd58836790921eb6305d661b0fb5ded43ca175051

 ![Dirección y ETH](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio1/1.png "Dirección y ETH")

Una vez abierta la consola de Ethereum cargué el archivo ensutils-testnet.js:

![Carga de archivo ensutils-testnet.js modificado para Rinkeby](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio1/2.png "Carga de archivo ensutils-testnet.js modificado para Rinkeby")

Después comprobé que el nombre que quería registrar no tenía dueño:

`new Date(testRegistrar.expiryTimes(web3.sha3('mywritten')).toNumber() * 1000)`

La respuesta fue: <Date Thu, 01 Jan 1970 01:00:00 CET>. Lo que significa que estaba libre. 

A continuación, registré el dominio en ENS: 

`testRegistrar.register(web3.sha3('mywritten'), eth.accounts[0], {from: eth.accounts[0]})`

Lo que me devolvió el siguiente hash: 0x11ff4a0ef16cb07e7b2fdb9537a3b7145adf24dd3288985e906e8913467c3054.

A continuación ordené a ENS a utilizar el public resolver para mi nombre de dominio:

`ens.setResolver(namehash('mywritten.test'), publicResolver.address, {from: eth.accounts[0]})`

Para comprobar que la transacción se había minado fui a etherscan:

![Transacción minada](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio1/3.png "Transacción minada")

Asimismo, pude comprobar que la transsacción se había operado en el cliente geth:

![Transacciones en Geth](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio1/4.png "Transacciones en Geth")

Una vez comprobado que se había minado mi transacción procedí a solicitar al Resolver a "resolver" el nombre de dominio para mi cuenta:

`publicResolver.setAddr(namehash('mywritten.test'), eth.accounts[0], {from: eth.accounts[0]})`

Lo que me devolvió el siguiente hash de la transacción: 0xb5b113a266a38ee23c699ced015650bd387eeed50603d807abfbad09e3b4a523

![Vinculación de cuenta con nombre de dominio](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio1/5.png "Vinculación de cuenta con nombre de dominio")

Para comprobar la vinculación de mi address con el nombre de dominio ejecuté las siguientes instrucciones:

`getAddr('mywritten.test')`

`resolverContract.at(ens.resolver(namehash('mywritten.test'))).addr(namehash('mywritten.test'))`

Para ambas instrucciones el resultado fue mi address: 0xd58836790921eb6305d661b0fb5ded43ca175051. Por tanto, soy la propietaria del dominio. 

![Comprobación de dominio](https://github.com/anakb/dev-pec2.2/blob/master/ejercicio1/6.png "Comprobación de dominio")


