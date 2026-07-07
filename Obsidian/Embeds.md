```base
filters:
  and:
    - file.hasTag("MaxximManufacturing")
views:
  - type: table
    name: Table
    sort:
      - property: file.name
        direction: DESC
  - type: cards
    name: View
    image: note.cssclasses
    imageFit: ""

```
Daniel
