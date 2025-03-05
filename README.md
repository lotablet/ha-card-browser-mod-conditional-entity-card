# **Una card per Home Assitant che raggruppa e mostra i dispositivi in base allo stato.**

Necessari i seguenti componenti da HACS:
  - **Browser Mod**
  - **Mushroom Card**

Il gruppo di luci e sensore li trovate sopra da inserire all'interno di **configuration.yaml** e inserendo le vostre luci di tutta la casa.

## Attenzione: Ho inserito dei commenti "//" per far capire il funzionamento della card, potete cancellarli una volta capito il funzionamento della card.

```
type: custom:mushroom-chips-card
alignment: center
chips:
  - content: |-
      {% if states('light.gruppo_luci_casa') == "on" %}     // Gruppo luci casa
        {{ states('sensor.counter_luci_accese') }}          // Sensore Template luci accese 
      {% else %}
        {{ states('sensor.counter_luci_accese') }}          // Sensore template luci accese 
      {% endif %}
    entity: light.gruppo_luci_casa                          // Gruppo luci casa
    icon: phu:bulbs-classic
    icon_color: |-
      {% if states('light.gruppo_luci_casa') == "on" %}     // Gruppo luci casa
       yellow 
      {% endif %}
    tap_action:
      action: fire-dom-event
      browser_mod:
        service: browser_mod.popup
        data:
          title: Luci Accese                                //Titolo della card
          content:
            type: vertical-stack
            cards:
              - type: conditional                           //Inizio codice
                conditions:
                  - entity: light.pulsante_sgabuzzino       //Nome entità 
                    state: "on"                             //Stato
                card:
                  type: custom:mushroom-entity-card
                  entity: light.pulsante_sgabuzzino         //Nome entità 
                  name: Luce Sgabuzzino
                  hold_action:
                    action: more-info
                  tap_action:
                    action: toggle                          //Fine codice
          size: fullscreen                                  // Dimensione della finestra di browser mod (possibili modalità: normal, wide, fullscreen)
          dismissable: true
    type: template
```

Ora non ci basterà che ripetere il codice dal commento //Inizio codice al commento //Fine codice con tutte le entità che ci interessa vedere lo stato di ON sul popup.

Se ti piace il mio lavoro non scordarti di seguirmi su Tiktok e Youtube [LINK](https://linktr.ee/lotablet)
