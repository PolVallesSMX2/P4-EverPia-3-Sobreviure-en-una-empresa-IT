# Fase 3: Treball en grup
## Debat i Selecció: Cada parella presenta el seu esquema. El grup debat els pros i contres de cada proposta (cost, temps de recuperació, seguretat, simplicitat).
Les dues propostes estan d’acord en prioritzar les dades més crítiques (bases de dades, documents de projecte, carpetes personals) i no incloure còpia completa dels equips clients, només carpetes clau.
L’esquema de la parella Pol i Pau pot ser més fàcil de implementar i administrar diàriament, amb una recuperació ràpida per a la majoria d’incidents i un cost assumible per una empresa petita.
L’esquema de Xavi/Blai aprofundeix en la periodicitat adaptada a RPO/RTO, i inclou opcions de còpia a llarg termini i diversificació de mitjans que incrementen robustesa, però amb més complexitat i cost.
## Disseny de la Política Final: El grup ha de redactar la Política de Còpies de Seguretat Definitiva que presentaran a l'empresa "Muntatges i Serveis Tècnics SL".
A Muntatges i Serveis Tècnics SL es garanteix la protecció de les dades més rellevants, incloent documents de projectes, la base de dades de Comptabilitat i Clients i les carpetes personals dels usuaris.
Les còpies es realitzaran de la següent manera: les dades de Comptabilitat i Clients tindran còpies incrementals diàries i una còpia completa setmanal. La documentació i les carpetes personals dels usuaris disposaran de còpies diferencials diàries, i un cop al mes es farà una còpia completa de totes les dades per assegurar la retenció mínima d’un mes.
El mitjà principal serà un NAS ubicat a l’oficina, que permet una recuperació ràpida de la informació. A més, es mantindrà una còpia addicional al Cloud per garantir recuperació fora del lloc en cas d’incident greu. Aquesta política assegura la disponibilitat i seguretat de les dades, complint amb els requisits de l’empresa.

# Document Final (Fase 3)
## Dades Objecte de Còpia

Per part del servidor haurem d'aplicar les següents questions:

| Tipus de Dada | Crítica | Freqüència de Còpia |
|--------------|---------|-------------------|
| Bases de Dades (Comptabilitat/Clients) | ☑ | Incremental cada 4 h + completa diària |
| Documents de Projectes | ☑ | Incremental diària + completa setmanal |
| Carpetes Personals dels Usuaris | ✕ | Incremental diària + completa setmanal |

Per part dels equips dels clients haurem d'aplicar les següents questions:

| Tipus de Dada | Crítica | Freqüència de Còpia |
|--------------|---------|-------------------|
| Documents locals temporals | ✕ | No es copia (es recomana guardar al servidor) |
| Configuracions especials | ☑ (si n'hi ha) | Còpia puntual si són difícils de recuperar |

Quines dades es copien i amb quina freqüència (separant Servidor/Clients i crítiques/no crítiques).

**Servidor:**

- Dades crítiques: Base de dades de Comptabilitat i Clients, documents de projectes → còpia incremental diària, còpia completa setmanal, còpia mensual completa.
- Dades no crítiques: Carpetes personals dels usuaris → còpia diferencial diària, còpia mensual completa.

**Clients:**

- Dades crítiques: Només les carpetes clau dels tècnics → còpia diferencial diària, còpia mensual completa.
- Dades no crítiques: La resta dels fitxers dels equips clients no es copien, ja que la informació important està centralitzada al servidor.
## Cronograma Setmanal Detallat

| Dia       | Dades (Ex: BD)                              | Tipus de còpia      | Mitjà        |
|-----------|---------------------------------------------|-------------------|-------------|
| Dilluns   | Comptabilitat/Clients, documents de projectes | Incremental       | NAS         |
|           | Carpetes personals dels usuaris              | Diferencial       | NAS         |
| Dimarts   | Comptabilitat/Clients, documents de projectes | Incremental       | NAS         |
|           | Carpetes personals dels usuaris              | Diferencial       | NAS         |
| Dimecres  | Comptabilitat/Clients, documents de projectes | Incremental       | NAS         |
|           | Carpetes personals dels usuaris              | Diferencial       | NAS         |
| Dijous    | Comptabilitat/Clients, documents de projectes | Incremental       | NAS         |
|           | Carpetes personals dels usuaris              | Diferencial       | NAS         |
| Divendres | Comptabilitat/Clients, documents de projectes | Incremental       | NAS         |
|           | Carpetes personals dels usuaris              | Diferencial       | NAS         |
| Dissabte  | Comptabilitat/Clients, documents de projectes | Incremental       | NAS         |
|           | Carpetes personals dels usuaris              | Diferencial       | NAS         |
| Diumenge  | Còpia completa de tot el servidor i dades clients | Completa         | NAS + Cloud |

## Elecció de Mitjans i Ubicació (Regla 3-2-1)

**- Mitjà 1 (Local):** NAS ubicat a l’oficina, que emmagatzema totes les còpies de manera centralitzada i permet una recuperació ràpida de la informació.
**- Mitjà 2 (Extern):** Cloud, utilitzant un servei segur com Microsoft Azure o Google Cloud, per garantir còpia fora del lloc i alta disponibilitat.
**- Ubicació Fora de Lloc:** La còpia externa es guarda al Cloud, gestionada pel proveïdor del servei i supervisada pel responsable de sistemes de l’empresa per assegurar accessibilitat i seguretat en cas d’incident.

## Estratègia de Recuperació (RTO/RPO)

Per garantir que les dades de Comptabilitat i Clients compleixen amb un RPO de 4 hores, es realitzen còpies incrementals diàries que capturen els canvis més recents i minimitzen la pèrdua de dades.
Per assolir un RTO de 4 hores, la recuperació es fa des del NAS local per obtenir accés immediat, amb la còpia al Cloud com a alternativa en cas que el servidor local no estigui disponible. Això garanteix que les dades es puguin recuperar ràpidament i que els problemes afectin poc el funcionament de l’empresa.
