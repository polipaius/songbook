# CLAUDE.md — Regole mobile web

Questa repo produce interfaccia web usata da mobile. Prima di considerare finito un lavoro sull'interfaccia, verifica sempre i punti qui sotto. Sono nate da due bug concreti (pulsante Salva finito sotto l'orologio, e zoom automatico entrando in un campo di testo) e servono a non ripeterli.

## 1. Safe area (orologio, notch, home indicator)

- Il `<meta viewport>` deve avere `viewport-fit=cover`.
- Ogni elemento in `position:fixed` o `position:sticky` ancorato a un bordo rispetta le safe area:
  - alto: `padding-top:env(safe-area-inset-top)`
  - basso: `padding-bottom:env(safe-area-inset-bottom)` oppure `bottom:calc(<valore> + env(safe-area-inset-bottom))`
  - lati: `max(<valore>px, env(safe-area-inset-left))` / `env(safe-area-inset-right)`
- Vale per TUTTI gli header, comprese schermate a tutto schermo, overlay e modali, non solo la barra principale. Un pulsante di azione (Salva, Chiudi, Annulla) non deve mai finire sotto l'orologio o il notch.

## 2. Niente zoom automatico quando si scrive

- Ogni `input`, `textarea` e `select` ha `font-size` minimo di 16px. Sotto i 16px iOS Safari zooma da solo al focus del campo.
- Attenzione alle regole che sovrascrivono il font solo su un campo (es. una textarea monospace): anche quella deve restare a 16px o più.
- Risolvi con i 16px, non con `maximum-scale=1` o `user-scalable=no`. Bloccare il pinch-zoom toglie all'utente la possibilità di ingrandire i contenuti a mano.

## 3. Altro mobile essenziale

- Aree tap almeno 44x44px.
- Sui bottoni: `-webkit-tap-highlight-color:transparent` e `touch-action:manipulation`, per togliere il flash grigio e il ritardo del doppio tap.
- Prova a 375px di larghezza: la pagina non deve scrollare in orizzontale. I contenuti larghi (tabelle, tab accordi, blocchi di codice) vanno in un contenitore con `overflow-x:auto`.
