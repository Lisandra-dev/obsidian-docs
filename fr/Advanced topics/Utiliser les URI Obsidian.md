Obsidian supporte un protocole URI personnalisé `obsidian://` qui peut être utilisé pour déclencher diverses actions dans l'application. Ceci est couramment utilisé sur MacOS et les applications mobiles pour l'automatisation et les flux de travail inter-applications.

Si vous avez installé Obsidian, ce lien ouvrira l'application sur votre appareil : [Cliquez ici](obsidian://open)

## Installation de l'URI d'Obsidian

Pour s'assurer que votre système d'exploitation redirige les URIs `obsidian://` vers l'application Obsidian, il peut y avoir des étapes supplémentaires que vous devez effectuer.

- Sous Windows, lancer l'application une fois devrait être suffisant. Cela enregistrera le gestionnaire de protocole personnalisé `obsidian://` dans le registre de Windows.
- Sous MacOS, exécuter l'application une fois devrait suffire, mais votre application **doit** être la version 0.8.12 ou ultérieure du programme d'installation.
- Sous Linux, le processus est beaucoup plus complexe :
	- Premièrement, assurez-vous de créer un fichier `obsidian.desktop`. [Voir ici pour plus de détails](https://developer.gnome.org/documentation/guidelines/maintainer/integrating.html#desktop-files)
	- Assurez-vous que votre fichier desktop spécifie le champ `Exec` comme `Exec=executable %u`. Le `%u` est utilisé pour passer les URIs `obsidian://` à l'application.
	- Si vous utilisez l'installateur AppImage, vous devrez peut-être le décompresser en utilisant `Obsidian-x.y.z.AppImage --appimage-extract`. Ensuite, assurez-vous que la directive `Exec` pointe vers l'exécutable décompressé.

## Utiliser les URIs d'Obsidian

Les URIs d'Obsidian sont typiquement dans ce format :

```
obsidian://action?param1=valeur&param2=valeur
```

- Le `action` est généralement l'action que vous souhaitez effectuer.

### Encodage

==Important==

Assurez-vous que vos valeurs sont correctement codées en URI. Par exemple, les barres obliques `/` doivent être codées en tant que `%2F` et les espaces en tant que `%20`.

Ceci est particulièrement important car un caractère "réservé" mal codé peut casser l'interprétation de l'URI. [Voir ici pour plus de détails](https://en.wikipedia.org/wiki/Percent-encoding)

### Actions disponibles

#### Action `open`

Description : Ouvre un coffre-fort Obsidian, et éventuellement un fichier dans ce coffre-fort.

Paramètres possibles :

- `vault` peut être soit le nom de l'espace de stockage, soit l'ID de l'espace de stockage.
	- Le nom de la chambre forte est simplement le nom du dossier de la chambre forte.
	- L'ID de la chambre forte est le code aléatoire de 16 caractères attribué à la chambre forte. Cet ID est unique pour chaque dossier de votre ordinateur. Exemple : `ef6ca3e3b524d22f`. Il n'y a pas encore de moyen facile de trouver cet ID, un moyen sera offert plus tard dans le commutateur de coffre-fort. Actuellement, il peut être trouvé dans `%appdata%/obsidian/obsidian.json` pour Windows. Pour MacOS, remplacez `%appdata%` par `~/Library/Application Support/`. Pour Linux, remplacez `%appdata%` par `~/.config/`.
- `file` peut être soit un nom de fichier, soit un chemin depuis la racine du coffre jusqu'au fichier spécifié.
	- Pour résoudre le fichier cible, Obsidian utilise le même système de résolution de liens qu'un `[[wikilink]]` ordinaire dans le coffre.
	- Si l'extension du fichier est `md`, l'extension peut être omise.
- `path` un chemin absolu du système de fichiers vers un fichier.
	- L'utilisation de ce paramètre remplacera à la fois `vault` et `file`.
	- L'application recherchera le coffre le plus spécifique qui contient le chemin d'accès au fichier spécifié.
	- Ensuite, le reste du chemin remplace le paramètre `file`.

Exemples :

- `obsidian://open?vault=my%20vault`
	Cette commande ouvre le coffre-fort "mon coffre-fort". Si le coffre-fort est déjà ouvert, mettez le focus sur la fenêtre.

- `obsidian://open?vault=ef6ca3e3b524d22f`
	Cette commande ouvre le coffre identifié par l'ID `ef6ca3e3b524d22f`.

- `obsidian://open?vault=my%20vault&file=my%20note`
	Cette commande ouvre la note "ma note" dans le coffre "mon coffre", en supposant que "ma note" existe et que le fichier est "ma note.md".

- `obsidian://open?vault=my%20vault&file=my%20note.md`
	Cela ouvre également la note `ma note` dans le coffre `mon coffre`.

- `obsidian://open?vault=my%20vault&file=path%2Fto%2Fmy%20note`
	Cette commande ouvre la note située à l'adresse `path/to/my note` dans le coffre `my vault`.

- `obsidian://open?path=%2Fhome%2Fuser%2Fmy%20vault%2Fpath%2Fto%2Fmy%20note`
	Cette commande recherchera tous les coffres qui contiennent le chemin `/home/user/my vault/path/to/my note`. Ensuite, le reste du chemin est passé au paramètre `file`. Par exemple, si un coffre existe à l'adresse `/home/user/my vault`, alors ceci serait équivalent au paramètre `file` défini à `path/to/my note`.

- `obsidian://open?path=D%3A%5CDocuments%5CMy%20vault%5CMy%20note`
	Cette commande recherchera tous les coffres contenant le chemin `D:\Documents\Mon coffre\Ma note`. Ensuite, le reste du chemin est passé au paramètre `file`. Par exemple, si un coffre-fort existe à l'adresse `D:\Documents\Mon coffre-fort`, cela équivaut à un paramètre `file` défini sur `Ma note`.

#### Action `search`

Description : Ouvre le volet de recherche d'un coffre-fort, et éventuellement effectue une requête de recherche.

Paramètres possibles :

- `vault` peut être soit le nom de l'espace de stockage, soit l'ID de l'espace de stockage. Identique à l'action `open`.
- `query` (facultatif) La requête de recherche à effectuer.

Exemples :

- `obsidian://search?vault=my%20vault`
	Cette action ouvre le coffre-fort "mon coffre-fort", et ouvre le volet de recherche.
- `obsidian://open?vault=ef6ca3e3b524d22f`
	Cette commande ouvre le coffre identifié par l'ID `ef6ca3e3b524d22f`.

- `obsidian://open?vault=my%20vault&file=my%20note`
	Cette commande ouvre la note "ma note" dans le coffre "mon coffre", en supposant que "ma note" existe et que le fichier est "ma note.md".

- `obsidian://open?vault=my%20vault&file=my%20note.md`
	Cela ouvre également la note `ma note` dans le coffre `mon coffre`.

- `obsidian://open?vault=my%20vault&file=path%2Fto%2Fmy%20note`
	Cette commande ouvre la note située à l'adresse `path/to/my note` dans le coffre `my vault`.

- `obsidian://open?path=%2Fhome%2Fuser%2Fmy%20vault%2Fpath%2Fto%2Fmy%20note`
	Cette commande recherchera tous les coffres qui contiennent le chemin `/home/user/my vault/path/to/my note`. Ensuite, le reste du chemin est passé au paramètre `file`. Par exemple, si un coffre existe à l'adresse `/home/user/my vault`, alors ceci serait équivalent au paramètre `file` défini à `path/to/my note`.

- `obsidian://open?path=D%3A%5CDocuments%5CMy%20vault%5CMy%20note`
	Cette commande recherchera tous les coffres contenant le chemin `D:\Documents\Mon coffre\Ma note`. Ensuite, le reste du chemin est passé au paramètre `file`. Par exemple, si un coffre-fort existe à l'adresse `D:\Documents\Mon coffre-fort`, cela équivaut à un paramètre `file` défini sur `Ma note`.

#### Action `search`

Description : Ouvre le volet de recherche d'un coffre-fort, et éventuellement effectue une requête de recherche.

Paramètres possibles :

- `vault` peut être soit le nom de l'espace de stockage, soit l'ID de l'espace de stockage. Identique à l'action `open`.
- `query` (facultatif) La requête de recherche à effectuer.

Exemples :

- `obsidian://search?vault=my%20vault`
	Cette action ouvre le coffre-fort "mon coffre-fort", et ouvre le volet de recherche.

- `obsidian://search?vault=my%20vault&query=MOC`
	Cette action ouvre le coffre-fort "mon coffre-fort", ouvre le volet de recherche et effectue une recherche sur "MOC".
	
#### Action `new`

Description : Crée une nouvelle note dans l'espace de stockage, avec éventuellement un contenu.

Paramètres possibles :

- `vault` peut être soit le nom de l'espace de stockage, soit l'ID de l'espace de stockage. Comme l'action `open`.
- `name` le nom du fichier à créer. Si cela est spécifié, l'emplacement du fichier sera choisi en fonction de vos préférences "Emplacement par défaut des nouvelles notes".
- `file` un chemin absolu du coffre, incluant le nom. Remplacera `name` s'il est spécifié.
- `path` un chemin absolu global. Fonctionne de manière similaire à l'option `path` de l'action `open`, qui remplacera à la fois `vault` et `file`.
- `content` (optionnel) le contenu de la note.
- `silent` (optionnel) définissez ceci si vous ne voulez pas ouvrir la nouvelle note.
- `append` (optionnel) ajouter à un fichier existant s'il en existe un.
- `overwrite` (optionnel) écrase un fichier existant s'il existe, mais seulement si `append` n'est pas défini.
- `x-success` (facultatif) voir [[#x-callback-url]].

Exemples :

- `obsidian://new?vault=my%20vault&name=my%20note`
	Ceci ouvre le coffre-fort "mon coffre-fort", et crée une nouvelle note appelée "ma note".
- `obsidian://new?vault=my%20vault&path=path%2Fto%2Fmy%20note`
	Cette action ouvre le coffre-fort "mon coffre-fort", et crée une nouvelle note à l'adresse "chemin/vers/ma note".
	
#### Action `hook-get-address` (recherche d'adresse)

Description : Point final à utiliser avec [Hook](https://hookproductivity.com/). Utilisation : `obsidian://hook-get-address`

Si `x-success` est défini, cette API l'utilisera comme x-callback-url. Sinon, elle copiera un lien markdown de la note en cours dans le presse-papiers, comme une URL `obsidian://open`.

Paramètres possibles :

- `vault` (optionnel) peut être soit le nom de l'espace de stockage, soit l'ID de l'espace de stockage. S'il n'est pas fourni, l'espace de stockage actuel ou le dernier espace de stockage ciblé sera utilisé.
- `x-success` (facultatif) voir [[#x-callback-url]].
- `x-error` (facultatif) voir [[#x-callback-url]].

## x-callback-url

Disponible depuis la version 0.14.3.

Certains endpoints accepteront les paramètres x-callback-url `x-success` et `x-error`. Quand il est fourni, Obsidian fournira les éléments suivants au callback `x-success` :
- `name` le nom du fichier, sans l'extension.
- `url` l'URI `obsidian://` pour ce fichier.
- `file` (desktop uniquement) l'URL `file://` de ce fichier.

Par exemple, si nous recevons
`obsidian://.....x-success=myapp://x-callback-url`
La réponse pourrait être
`myapp://x-callback-url?name=...&url=obsidian%3A%2F%2Fopen...&file=file%3A%2F%2F...`

## Formats abrégés

En plus des formats ci-dessus, il y a deux autres formats "sténographiques" disponibles pour ouvrir les coffres et les fichiers :

- `obsidian://vault/my vault/my note` est équivalent à `obsidian://open?vault=my%20vault&file=my%20note`
- `obsidian:///absolute/path/to/my note` est équivalent à `obsidian://open?path=%2Fabsolute%2Fpath%2Fto%2Fmy%20note`

Traduit avec www.DeepL.com/Translator (version gratuite)

