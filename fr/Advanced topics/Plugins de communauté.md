Obsidian autorise les développeurs à écrire des plugins communautaires pour étendre les fonctionnalités d'Obsidian.
Pour l'instant, l'API des plugins est en statut Alpha. Cela signifie que n'importe quelle partie de l'API peut introduire des modifications importantes dans des futures versions.

### Pour les développeurs

Pour obtenir des instructions sur la création de nouveaux plugins, consultez [notre exemple de plugin](https://github.com/obsidianmd/obsidian-sample-plugin).[^1]
Pour obtenir de la documentation sur l'API, consultez [le dépôt de l'API](https://github.com/obsidianmd/obsidian-api).[^2]

Après avoir créé votre plugin, vous pouvez l'ajouter à notre marché communautaire de plugin en créant une demande via un Pull Request dans [notre dépôt de version](https://github.com/obsidianmd/obsidian-releases). Consultez l'exemple de plugin pour savoir comment publier les mises à jour de votre plugin.

### Pour les utilisateurs
#### Le mode sans échec

Par défaut, le mode sans échec d'Obsidian est activé pour vous protéger de tout dommage potentiel. En mode sans échec, aucun plugin tiers ne sera éxécuté.

Sachez que les plugins tiers peuvent accéder aux fichiers de votre ordinateur, se connecter à internet et même installer des programmes supplémentaires. Pour en savoir plus sur la sécurité des plugins, [[#Sécurité des plugins|voyez ici]].

Afin d'installer les plugins tiers, vous devez désactiver le mode sans échec dans Paramètres → Plugin communautaire → Mode sans échec.

#### Découvrir et installer les plugins communautaires

Après avoir désactivé le mode sans échec, vous pouvez trouver les plugins tiers créés par la communauté dans Paramètres → Plugins tiers → plugins communautaires → Parcourir.

Sur cette page, vous pouvez parcourir les plugins par popularité, ou rechercher des plugins spécifiques. Cliquez sur un plugin pour voir les détails et les instructions de l'auteur du plugin. Dans la page de détails, vous pouvez cliquer sur "Installer" pour installer un plugin.

Après l'installation, vous trouverez les plugins installés sous Paramètres →  Plugin tiers. Ils doivent être activés pour prendre effet. Vous pouvez également les désinstaller à cet endroit.

## Sécurité des plugins

Merci de faire confiance à Obsidian pour vos données ! Cela signifie beaucoup pour nous, et nous prenons la sécurité très au sérieux. Cela inclut par ailleurs les plugins tiers.

Pour des raisons techniques avec notre plateforme, nous ne sommes pas en mesure de restreindre les plugins à un niveau de permission ou d'accès spécifique. Comme nous offrons Obsidian gratuitement, nous ne sommes pas en mesure de vérifier manuellement chaque plugin.

La bonne nouvelle est que Obsidian a une communauté incroyable et passionnée, donc nous comptons sur la confiance de la communauté pour assurer la sécurité des plugins tiers.

En général, vous devriez être en mesure de faire confiance à la plupart des plugins populaires de la communauté. **Si vous travaillez avec des données sensibles, nous vous recommandons d'inspecter le code du plugin avant de l'installer, afin que vos besoins en matière de sécurité soient satisfaits**. Vous pouvez trouver un lien vers le dépôt du plugin sur la page de détail du plugin.

Si vous trouvez des failles de sécurité dans les plugins communautaires, contactez l'auteur du plugin en ajoutant un problème sur GitHub. Si vous pensez que le plugin est malveillant, contactez-nous pour que le plugin soit examiné et supprimé.


[^1]: En anglais
[^2]: En anglais