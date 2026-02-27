# GPO Windows Server

## Pour modifier le fond d'ecran : 
Editeur de gestion des stratègies de groupes : 
* Configuration utilisateur > Strategies > Modeles d'administration > Bureau > Papier Peint du Bureau (Mettre le chemin du fond d'ecran)

## GPO  Configuration WSUS

**WSUS - Communs :**
* Configuration Ordinateur > Strategies > Parametres d'administration > Composants Windows > Windows Update
  * Specifier l'emplacement intranet du service de mise a jour Microsoft
`http://{nom_du_serveur}.{nom_du_domaine}:8530` (port du service WSUS)
  * Configuration du service des mises a jour automatiques **Modification des parametres a la convenance**
  * Ne pas se connecter a des emplacements Internet Windows Update > `Activé`

**WSUS - PC :**
* Configuration Ordinateur > Strategies > Parametres d'administration > Composants Windows > Windows Update
  * Autoriser le ciblage coté client
  `Activé` - `PC` (**PC qui est le nom de l'OU ou se trouve les PC**)
  * Desactiver le redemarrage automatique pour les mises a jour > `Activé` (Choisir les horaires)


> Sur la machine client :
> - gpupdate /force
>   - redemarrer le PC
> - gpresult /r /scope computer (pour voir si les GPO sont appliqués sur > la machine)

## GPO Mot de Passe
* Configuration Ordinateur > Strategies > Parametres Windows > Parametres de securité > Strategie de Compte > Strategie de Mot de Passe

  * Durée de vie maximale : (Souvent fixé a 42-90)
  * Longueur Minimal : (au moins 12 caractéres)
  * Exigences de complexité : (3 categories sur 4)
  * Historique des mots de passe : (souvent fixé a 24)
> Pour verifier quel strategie de mot de passe est appliqué sur le PC il faut faire la commande `net accounts` en administrateur
