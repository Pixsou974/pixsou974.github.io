# 📘 Guide Complet de la Syntaxe Markdown

Ce document récapitule les commandes essentielles pour structurer vos pages.

---

## 1. Les Titres (Headings)
On utilise le symbole `#` suivi d'un espace.
# Titre H1
## Titre H2
### Titre H3
#### Titre H4

---

## 2. Mise en forme du texte
Le style s'applique en entourant le texte :
* **Gras** : `**texte**`
* *Italique* : `*texte*` ou `_texte_`
* ~~Barré~~ : `~~texte~~`
* **_Gras et Italique_** : `***texte***`

---

## 3. Listes
### Listes à puces (non ordonnées)
* Élément A
* Élément B
  * Sous-élément (appuyez sur Tab)

### Listes numérotées
1. Premier
2. Deuxième

### Listes de tâches (Checklist)
- [x] Tâche terminée
- [ ] Tâche à faire

---

## 4. Les Tableaux 📊
C'est la partie la plus technique. La deuxième ligne définit l'alignement.

| Caractéristique | Syntaxe | Rendu |
| :--- | :---: | ---: |
| **Gauche** | `:---` | Défaut |
| **Centré** | `:---:` | Milieu |
| **Droite** | `---:` | Fin |

> **Astuce :** Pas besoin d'aligner parfaitement les barres verticales `|` dans votre code, GitHub s'occupe de la mise au propre !

---

## 5. Code et Blocs
### Code en ligne
Pour intégrer du `code` au milieu d'une phrase, utilisez un seul backtick : `` `code` ``.

### Blocs de code (Multi-lignes)
Utilisez trois backticks suivi du nom du langage pour la coloration :

```python
def hello():
    print("Hello World")
