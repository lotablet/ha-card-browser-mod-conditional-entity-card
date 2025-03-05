Una card per Home Assitant che raggruppa e mostra i dispositivi in base allo stato.

Necessari i seguenti componenti da HACS:
  - Browser Mod
  - Mushroom Card


Ho inserito i commenti "//" per far capire il funzionamento della card

Esempio:
```
type: custom:mushroom-chips-card
alignment: center
chips:
  - content: |-
      {% if states('light.gruppo_luci_casa') == "on" %}
        {{ states('sensor.counter_luci_accese') }}
      {% else %}
        {{ states('sensor.counter_luci_accese') }}
      {% endif %}
    entity: light.gruppo_luci_casa
    icon: phu:bulbs-classic
    icon_color: |-
      {% if states('light.gruppo_luci_casa') == "on" %}
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
Ora non ci basteràche ripetere il codice da //Inizio codice a //Fine codice con tutte le entità che ci interessa vedere lo stato di ON sul popup.
