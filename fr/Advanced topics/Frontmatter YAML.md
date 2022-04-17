---
aliases: front matter
---

YAML, également connu sous le nom de front matter, est conçu pour être des métadonnées au niveau du fichier qui sont lisibles par les humains *et* Obsidian.

Le front matter est une section d'attributs en texte brut qui commence à la première ligne du fichier. C'est l'une des façons les plus populaires d'ajouter des métadonnées dans un fichier Markdown, et elle a été popularisée par des générateurs statiques tels que Jekyll, Hugo et Gatsby.

Un bloc YAML a besoin de **triples tirets** au début et à la fin pour être lu par Obsidian (et d'autres applications). ==Il doit également être placé tout en haut du fichier. ==

Par exemple :

```
---
key : valeur
key2 : valeur2
clé3 : [un, deux, trois].
clé4 :
- quatre
- cinq
- six
---
```

Depuis la version 0.12.12, quatre clés sont supportées en natif :
- `tags` ([[Travailler avec les tags|plus information]])
- `aliases` ([[Ajouter des alias à une note|plus d'informations]])
- `cssclass`
- `publish` ([[Publier et dépublier des notes#Sélectionner automatiquement les notes à publier]] et [[Publier et dépublier des notes#Ignorer les notes]])

Comme Obsidian continue à se développer, nous le rendrons progressivement plus accessible aux développeurs de plugins, et le rendrons plus convivial.
