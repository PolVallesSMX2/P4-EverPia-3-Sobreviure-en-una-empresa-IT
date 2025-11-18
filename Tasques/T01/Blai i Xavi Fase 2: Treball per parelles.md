# Fase 2: Treball per parelles
##  Discussió i Consens: Comparen les seves respostes individuals (Fase 1).

| Aspecte | Resposta (Xavi) | Resposta (Blai) | Coincidències/ Diferències |
|---------|----------------|----------------|---------------------------|
| Què copiar | Bases de dades (prioritat màxima), documents de projectes, carpetes personals. No cal còpia completa dels 10 clients. | Bases de dades, documents, configuració del servidor, comptes d'usuari, permisos, màquines virtuals, logs. No cal còpia completa dels 10 clients. | Coincidim en no copiar tots els clients. En Xavi es centra en dades d'ús diari; en canvi en Blai, afegeix configuracions i logs. |
| Periodicitat | BD: Incremental cada 4 h + completa diària. Documents i carpetes: Incremental diària + completa setmanal. | Incremental diària (dilluns-divendres), diferencial setmanal (dissabte), completa mensual. | Diferència clara: en Xavi proposa còpies molt freqüents per complir RPO de 4 h; en canvi en Blai fa un esquema més "genèric" (incremental/diferencial/completa) però no compleix exactament el RPO. |
| Tipus de copia | Combines Incremental + completa (per BD i altres). | Incremental + diferencial + completa. | En Xavi adapta al RPO/RTO; en canvi el Blai aplica un esquema estàndard. |
| Mitjans i ubicació | NAS local + Cloud + discos externs (regla 3-2-1). | Discos externs + NAS + Cloud + cintes (regla 3-2-1). | En Xavi aplica la solució moderna/pràctica; en canvi en Blai, afegeix cintes per llarg termini. |

## Elaboració d'una Proposta Unificada: Heu de consensuar i dissenyar el vostre propi Esquema 3-2-1 de Còpies (3 còpies, 2 mitjans, 1 fora de lloc) basat en els requisits del cas.

| Aspecte | Resposta (Xavi) | Resposta (Blai) | Coincidències/ Diferències |
|---------|----------------|----------------|---------------------------|
| Què copiar | Bases de dades (prioritat màxima), documents de projectes, carpetes personals. No cal còpia completa dels 10 clients. | Bases de dades, documents, configuració del servidor, comptes d'usuari, permisos, màquines virtuals, logs. No cal còpia completa dels 10 clients. | Coincidim en no copiar tots els clients. En Xavi es centra en dades d'ús diari; en canvi en Blai, afegeix configuracions i logs. |
| Periodicitat | BD: Incremental cada 4 h + completa diària. Documents i carpetes: Incremental diària + completa setmanal. | Incremental diària (dilluns-divendres), diferencial setmanal (dissabte), completa mensual. | Diferència clara: en Xavi proposa còpies molt freqüents per complir RPO de 4 h; en canvi en Blai fa un esquema més "genèric" (incremental/diferencial/completa) però no compleix exactament el RPO. |
| Tipus de copia | Combines Incremental + completa (per BD i altres). | Incremental + diferencial + completa. | En Xavi adapta al RPO/RTO; en canvi el Blai aplica un esquema estàndard. |
| Mitjans i ubicació | NAS local + Cloud + discos externs (regla 3-2-1). | Discos externs + NAS + Cloud + cintes (regla 3-2-1). | En Xavi aplica la solució moderna/pràctica; en canvi en Blai, afegeix cintes per llarg termini. |

👉 [Torna a la pàguina de la tasca](README.md)  
📍 [Torna a la pàguina del projecte](../../README.md)
