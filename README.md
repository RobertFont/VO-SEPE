# VO-SEPE
Documentació d'integració del servei VO-SEPE del Consorci AOC.

**Índex**

- [VO-SEPE](#vo-sepe)
- [1 Introducció <a name="1"></a>](#1-introducció-)
- [2 Transmissions de dades disponibles <a name="2"></a>](#2-transmissions-de-dades-disponibles-)
- [3 Missatgeria dels serveis <a name="3"></a>](#3-missatgeria-dels-serveis-)
  - [3.1	Verificació de dades d’atur (VERIF_DADES_ATUR) <a name="3.1"></a>](#31verificació-de-dades-datur-verif_dades_atur-)
    - [3.1.1	Petició <a name="3.1.1"></a>](#311petició-)
    - [3.1.1.1	Dades genèriques](#3111dades-genèriques)
      - [3.1.1.2 Dades específiques](#3112-dades-específiques)
    - [3.1.2	Resposta – dades específiques <a name="3.1.2"></a>](#312resposta--dades-específiques-)
      - [3.1.2.1	Codis de resultat <a name="3.1.2.1"></a>](#3121codis-de-resultat-)
  - [3.2	Verificació d’imports actuals (VERIF_IMPORTS_ACTUALS) <a name="3.2"></a>](#32verificació-dimports-actuals-verif_imports_actuals-)
    - [3.2.1 Petició <a name="3.2.1"></a>](#321-petició-)
      - [3.2.1.1 Dades genèriques](#3211-dades-genèriques)
      - [3.2.1.2 Dades específiques](#3212-dades-específiques)
    - [3.2.2	Resposta – dades específiques <a name="3.2.2"></a>](#322resposta--dades-específiques-)
  - [3.3	Verificació d’imports per període (VERIF_IMPORTS_PERIODE) <a name="3.3"></a>](#33verificació-dimports-per-període-verif_imports_periode-)
    - [3.3.1 Petició <a name="3.2.1"></a>](#331-petició-)
      - [3.3.1.1 Dades genèriques](#3311-dades-genèriques)
      - [3.3.1.2 Dades específiques](#3312-dades-específiques)
    - [3.3.2	Resposta – dades específiques <a name="3.3.2"></a>](#332resposta--dades-específiques-)


# 1 Introducció <a name="1"></a>

Aquest document detalla la missatgeria associada al servei de l’Instituto Nacional de Empleo (INEM en endavant).

Per poder realitzar la integració cal conèixer prèviament la següent documentació:
•	Document d’Especificació de missatgeria pel consum de productes de la plataforma PCI del Consorci AOC.

# 2 Transmissions de dades disponibles <a name="2"></a>

Les dades disponibles a través del servei són les que es presenten a continuació:

| **EMISSOR** |
| --- |
| INEM (Instituto Nacional de Empleo) |

| **PRODUCTE** | **MODALITAT** | **DESCRIPCIO** | 
| --- | --- | --- |
| INEM | VERIF_DADES_ATUR | Informació sobre el certificat de la darrera situació de prestacions. |
| INEM | VERIF_IMPORTS_ACTUALS | Informació sobre el certificat d’imports actuals. |
| INEM | VERIF_IMPORTS_PERIODE | Informació sobre el certificat d’imports per període. |

Totes les consultes del producte tenen disponible la versió imprimible del resultat de la consulta en format PDF. Per més detalls adreceu-vos a l’apartat Extensions de missatgeria del document de missatgeria genèrica.

# 3 Missatgeria dels serveis <a name="3"></a>

A continuació es detalla la missatgeria corresponent al bloc de dades específiques de les modalitats de consum del producte INEM.

[image](https://user-images.githubusercontent.com/32306731/137331712-bc31edd6-6b5b-4372-977b-6230938c4af6.png) L’emissor de les dades requereix que s’informin les dades del funcionari que realitza la consulta. Així, cal informar els següents camps de l’element Funcionario del bloc de dades genèriques:

/Peticion/Funcionario/NombreCompletoFuncionario,
/Peticion/Funcionario/NifFuncionario,
//SolicitudTransmision/DatosGenericos/Solicitante/Funcionario/NombreCompletoFuncionario i
//SolicitudTransmision/DatosGenericos/Solicitante/Funcionario/NifFuncionario

## 3.1	Verificació de dades d’atur (VERIF_DADES_ATUR) <a name="3.1"></a>

La consulta de verificació de dades d’atur proporciona informació sobre el certificat de la darrera situació de prestacions.

### 3.1.1	Petició <a name="3.1.1"></a>

### 3.1.1.1	Dades genèriques 

| **ELEMENT** | **DESCRIPCIÓ** |  
| --- | --- |
| //DatosGenericos/Titular/TipoDocumentacion | Tipus de documentació (DNI / NIF o NIE). | 
| //DatosGenericos/Titular/Documentacion | Documentació. | 

#### 3.1.1.2 Dades específiques

Aquesta modalitat no requereix informar dades específiques.


### 3.1.2	Resposta – dades específiques <a name="3.1.2"></a>

La consulta de verificació de dades d’atur proporciona informació sobre el certificat de la darrera situació de prestacions.

De <i>l’schema</i> associat a la resposta especifica, el servei informa les dades que es detallen a continuació.

| **ELEMENT** | **DESCRIPCIÓ** |  
| --- | --- | 
| //DatosDesempleo/IPF | Identificador de persona física del SPEE (Servicio Público de Empleo Estatal) – INEM. | 
| //DatosDesempleo/indSituacion | Indicador de situació (SI / NO). Indica si l’INEM posseeix informació de prestacions del titular consultat. | 
| //DatosDesempleo/tiPres | Tipus de prestació. Descripció del tipus de prestació del darrer dret reconegut al beneficiari. |
| //DatosDesempleo/situacion | Situació de la prestació (ALTA / BAJA). ALTA: el ciutadà està cobrant la prestació d'atur. BAJA: el ciutadà no està cobrant la prestació d'atur. |
| //DatosDesempleo/fxInicioSituacion | Data d’inici de la situació actual del dret (format DDMMAAAA). En cas que situacion sigui ALTA, el camp indica la data inicial en que el titular va començar a cobrar la prestació d'atur. En cas que situacion sigui BAJA, indica la data inicial en que el titular va deixar de cobrar la prestació d'atur. |
| //DatosDesempleo/fxFinSituacion | Data de fi de la situació del dret (format DDMMAAAA). En cas que situacion sigui ALTA, aquest camp representa el període de cobrament concedit de la prestació; indica la data de finalització. En cas que situacion sigui BAIXA, aquest camp no s'informarà. |
| //DatosDesempleo/diasReconocidos | Número de dies reconeguts sobre el dret total. | 
| //DatosDesempleo/diasConsumidos | Número de dies consumits. | 
| //DatosDesempleo/baseRegula	| Base reguladora diària. | 
| //DatosDesempleo/cotizacion	| Base de contingències comuns. |
| //DatosDesempleo/cuentaCotiza	| Patronal de l’Inem. |
| //DatosDesempleo/indRetJudicial	| Indicador de retenció judicial. |
| //DatosDesempleo/indEmbargo	| Indicador d’embargament. |
| //DatosDesempleo/indCobroIndebido	| Indicador de cobrament indegut. Indica si els guanys del beneficiari estan sent compensats pel propi SPEE-INEM com a conseqüència d'una percepció indeguda anterior, en la seva totalitat o en part. |
| //resultat/codiResultat	| Codi de resultat de l’operació de consulta (vegeu apartat 0). |
| //resultat/descripcio	| Descripció del resultat. |

(Adjuntar imatge)

#### 3.1.2.1	Codis de resultat <a name="3.1.2.1"></a>

•	0003: Tramitada. Titular localitzat.
•	0231: Error reportat per l’emissor. Error de format documentació.
•	0232: Error reportat per l’emissor. Existeix més d’un registre per les dades proporcionades en la consulta.
•	0233: El titular de la consulta no existeix a la BBDD de l’INEM.
•	0238: No hi ha dades del titular consultat. El titular està enregistrat a la BBDD de l’INEM, però per la consulta efectuada no existeixen dades al moment de la consulta i, per tant, no és sol·licitant de la prestació consultada.
•	0502: Error en la comunicació amb l’emissor.

## 3.2	Verificació d’imports actuals (VERIF_IMPORTS_ACTUALS) <a name="3.2"></a>

Aquesta consulta proporciona informació sobre el certificat d’imports actuals.

### 3.2.1 Petició <a name="3.2.1"></a>

#### 3.2.1.1 Dades genèriques 

| **ELEMENT** | **DESCRIPCIÓ** |  
| --- | --- | 
| //DatosGenericos/Titular/TipoDocumentacion | Tipus de documentació (DNI / NIF o NIE). | 
| //DatosGenericos/Titular/Documentacion | Documentació. | 

#### 3.2.1.2 Dades específiques

Aquesta modalitat no requereix informar dades específiques.

### 3.2.2	Resposta – dades específiques <a name="3.2.2"></a>

De <i>l’schema</i> associat a la resposta especifica, el servei informa les dades que es detallen a continuació.

| **ELEMENT** | **DESCRIPCIÓ** |  
| --- | --- | 

| //DatosImporteActual/TIPRES | Descripció del tipus de prestació o subsidi del darrer dret reconegut al beneficiari. |
| //DatosImporteActual/FXINICIOSITUACION | Data d'inici de la situació actual del dret (format DD/MM/AAAA). |
| //DatosImporteActual/FXFINSITUACION | Data de fi de la situació del dret (format DD/MM/AAAA). Si està de baixa no tindrà valor. |
| //DatosImporteActual/BASEREGULA | Base reguladora diària. Correspon a la quantia diària que ha de percebre el beneficiari de la prestació (format ZZ,ZZ). |
| //DatosImporteActual/IMPBRUTO | Quantia de l'import brut (format Z.ZZZ.ZZZ,ZZ). |
| //DatosImporteActual/IMPREASS	 | Import de la quota fixa del REASS - Régimen Especial Agrario de la Seguridad Social (format Z.ZZZ.ZZZ,ZZ). |
| //DatosImporteActual/IMPIRPF | Import de la retenció a efectes de l'I.R.P.F (format
±ZZZ.ZZZ,ZZ). |
| //DatosImporteActual/IMPSEGSOC | 	Import descompte de la Seguretat Social (±ZZZ.ZZZ,ZZ). |
| //resultat/codiResultat | Codi de resultat de l’operació de consulta (vegeu apartat 0). |
| //resultat/descripcio	| Descripció del resultat. |

(Adjuntar imatge)

## 3.3	Verificació d’imports per període (VERIF_IMPORTS_PERIODE) <a name="3.3"></a>

Aquesta consulta proporciona informació sobre el certificat d’imports per període.

### 3.3.1 Petició <a name="3.2.1"></a>

#### 3.3.1.1 Dades genèriques 

| **ELEMENT** | **DESCRIPCIÓ** |  
| --- | --- |
| //DatosGenericos/Titular/TipoDocumentacion | 	Tipus de documentació (DNI / NIF o NIE). |
| //DatosGenericos/Titular/Documentacion | 	Documentació. |

#### 3.3.1.2 Dades específiques

| **ELEMENT** | **DESCRIPCIÓ** |  
| --- | --- | 
| /peticioVerificacioImportsPeriode/  | Data d’inici del període (MM/AAAA). |
| /DatosImportePeriodo/FXINICIO	 | Data d’inici del període (MM/AAAA). |
| /peticioVerificacioImportsPeriode/  | Data de fi del període (MM/AAAA). |
| /DatosImportePeriodo/FXFINAL	 | Data de fi del període (MM/AAAA). |

L’interval del període sobre el qual es fa la consulta ha de comprendre 12 mesos com a màxim.

### 3.3.2	Resposta – dades específiques <a name="3.3.2"></a>

De <i>l’schema</i> associat a la resposta especifica, el servei informa les dades que es detallen a continuació.

(Adjuntar imatge)

| **ELEMENT** | **DESCRIPCIÓ** |  
| --- | --- | 

| //DatosImportePeriodo/IPF	 | Identificador de persona física del SPEE (Servicio Público de Empleo Estatal) – INEM. |
| //DatosImportePeriodo/FXINICIO | 	Data d'inici del període (format MM/AAAA). |
| //DatosImportePeriodo/FXFINAL | 	Data de fi del període (format MM/AAAA). |
| //DatosImportePeriodo/IMPBRUTO | 	Quantia de l'import brut (format Z.ZZZ.ZZZ,ZZ). |
| //DatosImportePeriodo/IMPREASS | 	Import de la quota fixa del REASS - Régimen Especial Agrario de la Seguridad Social (format Z.ZZZ.ZZZ,ZZ). |
| //DatosImportePeriodo/IMPIRPF | 	Import de la retenció a efectes de l'I.R.P.F (format
±ZZZ.ZZZ,ZZ). |
| //DatosImportePeriodo/IMPSEGSOC | 	Import descompte de la Seguretat Social (±ZZZ.ZZZ,ZZ). |
| //resultat/codiResultat | Codi de resultat de l’operació de consulta (vegeu apartat 0). |
| //resultat/descripcio | 	Descripció del resultat. |





