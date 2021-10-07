# e-TAULER
Document d’integració del servei.

Podreu trobar els XSD's del servei en aquest repositori sota el directori [/schema](https://github.com/ConsorciAOC/e-TAULER/tree/main/schema).

## Control del document

### Informació general
| **Títol:** | E-TAULER. Document d&#39;integració del servei |
| --- | --- |
| **Creat per:** | Àrea de Tecnologia - Projectes |
| **A revisar per:** | Àrea de Tecnologia - Suport |
| **A aprovar per:** | Àrea de Tecnologia - Suport |
| **Llista de distribució:** ||
| **Nom del document:** | DI - Modalitats E-TAULER.doc |


### Històric de revisions
| **Versió** | **Data** | **Autor** | **Comentaris** |
| --- | --- | --- | --- |
| V1.0 | 05/11/2013 | Roger Noguera i Arnau | Creació del document. Versió 3.0. |
| V1.1 | 13/01/2015 | Roger Noguera i Arnau | Funcionalitats versió 1er trimestre 2015 |
| V1.2 | 19/11/2015 | Roger Noguera i Arnau | Edictes destacats. |
| V1.3 | 03/09/2019 | Roger Noguera i Arnau | Esmenes. |

### Índex

TODO

## 1 Introducció <a name="1"></a>

Aquest document detalla la missatgeria associada al servei E-TAULER.

Per poder realitzar la integració cal conèixer prèviament la següent documentació:

- Document d&#39;_Especificació de missatgeria pel consum de productes de la plataforma PCI_ del Consorci AOC.

## 2 Transmissions de dades disponibles <a name="2"></a>
Les dades disponibles a través del servei són les que es presenten a continuació:
- **EMISSOR**: CAOC (Consorci Administració Oberta de Catalunya)

| **PRODUCTE** | **MODALITAT** | **DESCRIPCIO** |
| --- | --- | --- |
| **ETAULER** | ETAULER | Operacions publicades pel servei E-TAULER: <ul><li>Publicar un edicte.</li><li>Cancel·lar un edicte pendent de publicar.</li><li>Ampliar el termini de publicació d&#39;un edicte.</li><li>Destacar un edicte publicat.</li><li>Retirar un edicte publicat.</li><li>Sincronització: edictes que s&#39;han publicat i retirat.</li><li>Descàrrega de document (edicte / diligència).</li><li>Consulta d&#39;estat d&#39;un edicte.</li></ul>|

## 3 Missatgeria dels serveis <a name="3"></a>

A continuació es detalla la missatgeria corresponent al bloc de dades específiques de les diferents operacions publicades pel producte.

> :warning: Per aquest producte NO informeu l&#39;element IdSolicitanteOriginal de la missatgeria genèrica.

### 3.1 Publicar un edicte <a name="3.1"></a>
#### 3.1.1 Petició – dades genèriques <a name="3.1.1"></a>

El fitxer corresponent a la remesa s&#39;ha de referenciar al bloc de dades //Ficheros/Fichero de les dades genèriques de la sol·licitud.

| _Element_ | _Descripció_ |
| --- | --- |
| //Ficheros/Fichero/Contenido | Contingut del fitxer PDF de l&#39;edicte en cas de transferència per MTOM (en la crida correspon a la referència XOP del fitxer).|
| //Ficheros/Fichero/RutaFichero | Alternativa a Contenido, permet informa la ruta (ha de ser accessible per la plataforma PCI del CAOC) on es troba el fitxer (p.e. transferint-la prèviament per SFTP).|
| //Ficheros/Fichero/Id | Identificador de document PDF referenciat a la missatgeria específica (//edicte/document/id).|

#### 3.1.2 Petició – dades específiques <a name="3.1.2"></a>

| _Element_ | _Descripció_ |
| --- | --- |
| /peticioPublicarEdicte/edicte | Dades de l&#39;edicte a publicar.|

#### 3.1.3 Dades de l&#39;edicte <a name="3.1.3"></a>


| _Element_ | _Descripció_ |
| --- | --- |
| //edicte/idEdicte | Identificador alfanumèric de l&#39;identificador d&#39;edicte. Màxim fins a 256 caràcters.|
| //edicte/numExpedient | Identificador alfanumèric del número de l&#39;expedient de l&#39;edicte. Màxim fins a 256 caràcters. |
| //edicte/informacio | Bloc de dades corresponent a la informació de l&#39;edicte (un per idioma, català obligatori). |
| //edicte/informacio/titol | Títol de l&#39;edicte. Màxim fins a 256 caràcters. |
| //edicte/informacio/descripcio | Identificador alfanumèric de descripció de l&#39;edicte. Màxim fins a 4000 caràcters. |
| //edicte/informacio/idioma | Idioma: <ul><li>ca: català</li><li>es: castellà</li><li>oc: aranès</li></ul>|
| //edicte/dataIniciPublicacio | Data de l&#39;inici de la publicació de l&#39;edicte. |
| //edicte/dataFiPublicacio | Data fi de la publicació de l&#39;edicte (darrera data en la que l&#39;edicte estarà visible). Si no s&#39;informa l&#39;edicte tindrà un temps d&#39;exposició indefinit i per despublicar-lo caldrà realitzar una operació de retirada del mateix. |
| //edicte/destacat | L&#39;edicte és destacat? |
| //edicte/diligencia/idioma | Idioma per defecte de la diligència: <ul><li>ca: català</li><li>es: castellà</li><li>oc: aranès</li></ul> |
| //edicte/diligencia/format | Format per defecte de la diligència: <ul><li>electronica: versió electrònica</li><li>imprimible: versió imprimible</li></ul>|
| //edicte/document | Bloc de dades corresponent al document d&#39;un edicte (un per idioma, català obligatori). |
| //edicte/document/nom | Nom del document. |
| //edicte/document/id | El document PDF de l&#39;edicte es referència al bloc de dades Ficheros del bloc de dades genèriques de la sol·licitud. Així, aquest element id s&#39;ha de correspondre amb l&#39;element Fichero/Id on s&#39;especifica les dades per recuperar el contingut del document. |
| //edicte/document/idioma | Idioma del document: <ul><li>ca: català</li><li>es: castellà</li><li>oc: aranès</li></ul> |
| //edicte/edicteExtern/codiEnsOrigen | Camp alfanumèric per indicar el codi ens INE10 de l&#39;ens origen en els casos d&#39;edictes externs procedents de Catalunya. |
| //edicte/edicteExtern/nomEnsOrigen | Nom de l&#39;ens origen de l&#39;edicte en cas d&#39;edictes externs. |
| //edicte/edicteExtern/registreEntrada | Camp alfanumèric per indicar el registre d&#39;entrada de l&#39;edicte en cas d&#39;edictes externs. |
| //edicte/edicteExtern/dataRecepcio | Camp tipus data per indicar la data de recepció de l&#39;edicte en cas d&#39;edictes externs. |
| //edicte/classificacio | Bloc de dades corresponent a la classificació d&#39;un edicte. |
| //edicte/classificacio/tipus | Tipus: <ul><li>classificacio1: criteri de classificació 1.</li><li>classificacio2: criteri de classificació 2.</li><li>procedencia: procedència.</li></ul>|
| //edicte/classificacio/classificacio | Bloc de dades corresponent a les dades d&#39;un criteri de classificació (idioma català obligatori). |
| //edicte/classificacio/classificacio/concepte | Etiqueta descriptiva del criteri de classificació. |
| //edicte/classificacio/classificacio/categoria | Nom de la categoria. |
| //edicte/classificacio/classificacio/subcategoria | Nom de la subcategoria. |
| //edicte/classificacio/classificacio/idioma | Idioma: <ul><li>ca: català</li><li>es: castellà</li><li>oc: aranès</li></ul>|
| //edicte/dadesAddicionals/paraulesClau | Paraules clau per les que es podrà cercar l&#39;edicte a la part del ciutadà, separades per comes (&#39;,&#39;). |
| //edicte/dadesAddicionals/nifs | NIFs vinculats amb l&#39;edicte que es publica. |
| //edicte/dadesAddicionals/referencia | Referència externa vinculada a un edicte. |
| //dadesAddicionals/referencia/url | URL d&#39;una referència vinculada a l&#39;edicte. |
| //dadesAddicionals/referencia/seu | Indica si l&#39;enllaç forma part de la seu (per defecte, si no s&#39;informa, true). |
| //dadesAddicionals/referencia/enllaç/titol | Títol, descripció de la referència. |
| //dadesAddicionals/referencia/enllaç/idioma | Idioma:<ul><li>ca: català</li><li>es: castellà</li><li>oc: aranès</li></ul>|
| //dadesAddicionals/adjunt/id | El document adjunt es referència al bloc de dades Ficheros del bloc de dades genèriques de la sol·licitud. Així, aquest element id s&#39;ha de correspondre amb l&#39;element Fichero/Id on s&#39;especifica les dades per recuperar el contingut del document. |
| //dadesAddicionals/adjunt/enllac/titol | Títol, descripció de l&#39;adjunt. |
| //dadesAddicionals/adjunt/enllac/idioma | Idioma:<ul><li>ca: català</li><li>es: castellà</li><li>oc: aranès</li></ul> |
| //edicte/esmena | Bloc que indica que l&#39;edicte a publicar esmena un altre edicte. |
| //esmena/idEdicte | Identificador de l&#39;edicte que l&#39;edicte a publicar esmena. |
| //esmena/motiu/descripcio | Motiu de l&#39;esmena. |
| //esmena/motiu/idioma | Idioma:<ul><li>ca: català</li><li>es: castellà</li><li>oc: aranès</li></ul>|
