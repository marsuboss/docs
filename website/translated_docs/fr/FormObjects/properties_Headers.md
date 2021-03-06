---
id: propertiesHeaders
title: En-têtes
---

---
## Afficher en-têtes

This property is used to display or hide [list box column headers](listbox_overview.md#list-box-headers). There is one header per column; each header is configured separately.

#### Grammaire JSON

| Nom         | Type de données | Valeurs possibles |
| ----------- | --------------- | ----------------- |
| showHeaders | boolean         | true, false       |

#### Objets pris en charge

[List Box](listbox_overview.md)




---
## Hauteur

This property is used to set the row height for a list box header in **pixels** or **text lines** (when displayed). Les deux types d'unités peuvent être utilisés dans la même list box :

*   *Pixel* - la valeur de hauteur est appliquée directement à la ligne concernée, quelle que soit la taille de la police contenue dans les colonnes. Si une police est trop grande, le texte est tronqué. De plus, les images sont tronquées ou redimensionnées selon leur format.

*   *Ligne* - la hauteur est calculée en tenant compte de la taille de police de la ligne concernée.
    *   If more than one size is set, 4D uses the biggest one. For example, if a row contains "Verdana 18", "Geneva 12" and "Arial 9", 4D uses "Verdana 18" to determine the row height (for instance, 25 pixels). This height is then multiplied by the number of rows defined.
    *   This calculation does not take into account the size of pictures nor any styles applied to the fonts.
    *   In macOS, the row height may be incorrect if the user enters characters that are not available in the selected font. When this occurs, a substitute font is used, which may cause variations in size.
> This property can also be set dynamically using the [LISTBOX SET HEADERS HEIGHT](https://doc.4d.com/4Dv17R6/4D/17-R6/LISTBOX-SET-HEADERS-HEIGHT.301-4311129.en.html) command.

Conversion of units: When you switch from one unit to the other, 4D converts them automatically and displays the result in the Property List. For example, if the font used is "Lucida grande 24", a height of "1 line" is converted to "30 pixels" and a height of "60 pixels" is converted to "2 lines".

Note that converting back and forth may lead to an end result that is different from the starting value due to the automatic calculations made by 4D. This is illustrated in the following sequences:

*(font Arial 18)*: 52 pixels -> 2 lines -> 40 pixels *(font Arial 12)*: 3 pixels -> 0.4 line rounded up to 1 line -> 19 pixels

#### Exemple JSON :

```
    "List Box": {
        "type": "listbox",
        "showHeaders": true,
        "headerHeight": "22px",  
        ...
        }
```



#### Grammaire JSON

| Nom          | Type de données | Valeurs possibles               |
| ------------ | --------------- | ------------------------------- |
| headerHeight | string          | positive decimal+px &#124; em ) |

#### Objets pris en charge

[List Box](listbox_overview.md)


#### Voir également

[Footers](properties_Footers.md) - [List box headers](listbox_overview.md#list-box-headers)