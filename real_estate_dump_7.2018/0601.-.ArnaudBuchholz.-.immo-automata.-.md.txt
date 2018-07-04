# immo-automata
Automated real estate lookup with modular extractions, data consolidation


## How to create a configuration file

```JavaScript
{
    "extractors": [{
        "type": "centris",
        "id": "condo",
        "town": "Montréal",
        "suburb": "Tous les arrondissements",
        "max-price": 500000,
        "house-types": ["Condo", "Loft / Studio"],
        "room-type": "2+"
    }, {
        "type": "centris",
        "id": "condo",
    }]
}
```
