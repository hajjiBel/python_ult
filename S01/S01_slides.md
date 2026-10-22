---
marp: true
theme: default
paginate: true
size: 16:9
header: 'Python – Programmation, approche objet et bonnes pratiques'
footer: 'S1 · Présentation du langage et installation'
style: |
  section { font-family: 'Segoe UI', 'Helvetica Neue', Arial, sans-serif; font-size: 26px; color: #1f2933; padding: 50px 60px; }
  h1 { color: #1f4e78; font-size: 44px; }
  h2 { color: #1f4e78; font-size: 34px; border-bottom: 3px solid #f2b705; padding-bottom: 6px; }
  code { background: #eef2f7; color: #b3261e; border-radius: 4px; padding: 0 4px; }
  section pre { background: #f4f6f9 !important; border: 1px solid #d9e2ec; border-left: 5px solid #1f4e78; border-radius: 8px; font-size: 20px; }
  section pre code { background: transparent !important; color: #1f2933 !important; }
  table { font-size: 21px; }
  th { background: #1f4e78; color: #fff; }
  header, footer { color: #8a94a3; font-size: 14px; }
  section.title { background: linear-gradient(135deg, #1f4e78 0%, #2f6f9f 100%); color: #fff; }
  section.title h1, section.title h2 { color: #fff; border: none; }
  section.lab { background: #fff8e1; }
  section.lab h2 { border-color: #1f4e78; }
  .small { font-size: 20px; color: #52606d; }
---

<!-- _class: title -->
<!-- _paginate: false -->
<!-- _header: '' -->

# Séance 1
## Présentation du langage + atelier d'installation

**Objectifs de la séance**
- Situer Python : histoire, versions, usages
- Utiliser l'interpréteur interactif (REPL) et la documentation officielle
- Installer un environnement de travail complet : Python, IDE, venv, JupyterLab
- Écrire et exécuter un premier script et un premier notebook

<!--
Timing : 3 min.
Accueil, tour de table rapide (prénom, métier, langages déjà pratiqués) : noter les profils dev / chef de projet / data / admin sys pour adapter les exemples.
Annoncer le format : 18 séances, théorie courte puis pratique, projet fil rouge GestParc.
Remarque : pas de quiz flash en S1, les 10 min sont consacrées à l'accueil et au tour de table.
-->

---

## Plan de la séance

| Durée | Bloc |
|---|---|
| 10 min | Accueil et tour de table |
| 20 min | Théorie 1 : histoire, Python 2 vs 3, REPL, documentation, IDE |
| 30 min | 🧪 Atelier : installation + venv + premier script + premier notebook |
| 5 min | Pause |
| 20 min | Théorie 2 : instructions, commentaires, premières variables |
| 30 min | 🧪 Lab partie 2 + étape 0 du projet GestParc |
| 5 min | Récapitulatif |

<!--
Timing : 1 min.
Insister : l'atelier d'installation est le moment le plus important de la soirée. Tout le monde doit repartir avec un environnement qui fonctionne.
-->

---

## Python en quelques dates

| Année | Événement |
|---|---|
| 1989 | Guido van Rossum commence Python (nom tiré des *Monty Python*) |
| 1991 | Première version publique (0.9.0) |
| 2000 | Python 2.0 |
| 2008 | Python 3.0 : rupture volontaire de compatibilité |
| 2018 | Guido quitte le rôle de « BDFL », gouvernance par un *Steering Council* |
| 2020 | Fin de vie de Python 2 (dernière version : 2.7.18) |
| Depuis 2019 | Une nouvelle version 3.x chaque année en octobre (PEP 602) |

<p class="small">Nous travaillons en Python 3.12 ou plus récent.</p>

<!--
Timing : 3 min.
Question à poser : « Où avez-vous déjà croisé Python ? » (scripts d'admin, Ansible, data science, Django, IA...).
Message clé : langage mature (plus de 30 ans), gouvernance ouverte, versions régulières.
-->

---

## Pourquoi Python ?

- **Lisible** : la syntaxe ressemble à du pseudo-code, l'indentation fait partie du langage
- **Polyvalent** : un même langage pour des besoins très différents
- **Batteries included** : une bibliothèque standard très riche
- **Écosystème** : plus de 500 000 paquets sur PyPI

| Profil | Usage typique |
|---|---|
| Admin sys / réseau | Automatisation, Ansible, analyse de logs |
| Data | pandas, NumPy, Jupyter, machine learning |
| Développeur | Web (Django, FastAPI), outils, tests |
| Chef de projet | Scripts de reporting, extraction de données |

<!--
Timing : 2 min.
Adapter l'exemple au public présent (cf. tour de table).
Python est interprété : pas de compilation explicite, ce qui facilite l'expérimentation mais impose de bien tester.
-->

---

## Python 2 vs Python 3 : les différences visibles

| | Python 2 | Python 3 |
|---|---|---|
| Affichage | `print "Bonjour"` (instruction) | `print("Bonjour")` (fonction) |
| Division | `7 / 2` → `3` | `7 / 2` → `3.5` |
| Texte | ASCII par défaut | Unicode par défaut |
| Saisie | `raw_input()` | `input()` |
| Statut | **Fin de vie depuis 2020** | Version actuelle |

⚠️ Un tutoriel ou une réponse en ligne qui utilise `print "..."` sans parenthèses est **obsolète**.

<!--
Timing : 3 min.
Démo live éventuelle : taper print "x" dans un interpréteur Python 3 et montrer la SyntaxError avec le message "Did you mean print(...)?".
Point admin sys : de vieux scripts Python 2 traînent encore sur certains serveurs, il faut savoir les reconnaître.
-->

---

## L'interpréteur interactif (REPL)

**R**ead – **E**val – **P**rint – **L**oop : on tape, Python évalue et affiche.

```text
$ python
Python 3.12.7 (main, ...) on linux
>>> 2 + 3
5
>>> 7 / 2
3.5
>>> "Gest" + "Parc"
'GestParc'
>>> exit()
```

- Windows : `py` ou `python` · Linux / macOS : `python3`
- Quitter : `exit()` ou Ctrl+D (Linux/macOS), Ctrl+Z puis Entrée (Windows)

<!--
Timing : 3 min. Démo live obligatoire dans un terminal.
Montrer que le REPL affiche la valeur d'une expression sans print.
Montrer la flèche du haut pour rappeler une commande.
-->

---

## La documentation officielle

- **python.org** : téléchargements, actualités
- **docs.python.org/fr/3/** : documentation en français
  - *Tutoriel* : à lire en complément de la formation
  - *Référence de la bibliothèque standard* : à garder sous la main
- Dans le REPL :

```python
>>> help(print)      # aide sur une fonction
>>> import this      # le Zen of Python (on y reviendra en S14)
```

💡 Réflexe à prendre : **la documentation officielle avant le forum**.

<!--
Timing : 2 min.
Ouvrir docs.python.org/fr/3/ en direct et montrer le sélecteur de version et de langue.
help() : touche q pour quitter le pager.
-->

---

## Bien choisir son environnement de développement

| Outil | Points forts | Pour qui ? |
|---|---|---|
| **VS Code** + extensions Python et Jupyter | Léger, gratuit, multi-langages, notebooks intégrés | Tous (outil de référence de la formation) |
| **PyCharm** | Très complet, refactoring, debugger avancé | Développeurs |
| **JupyterLab** | Code + texte + graphiques, exécution par cellules | Data, exploration, labs |
| IDLE | Fourni avec Python | Dépannage seulement |

Nos labs : **notebooks** `.ipynb` · nos programmes : **scripts** `.py`

<!--
Timing : 3 min.
Laisser le choix VS Code / PyCharm, mais les démos se feront dans VS Code.
Script = programme complet exécuté de haut en bas ; notebook = exploration, cellules exécutables dans n'importe quel ordre (danger : l'ordre d'exécution compte !).
-->

---

## L'environnement virtuel (venv)

Un **venv** = une copie isolée de Python, propre à un projet.

```text
gestparc/
├── .venv/          ← Python + paquets du projet (ne pas versionner)
├── main.py
└── README.md
```

- Évite les conflits de versions entre projets
- Ne touche pas au Python du système (crucial sur Linux)
- Se crée en une commande : `python -m venv .venv`

<!--
Timing : 2 min.
Analogie : un venv, c'est comme un conteneur Docker léger, mais uniquement pour les paquets Python.
On détaillera pip et requirements.txt en S14 ; ce soir, on installe juste JupyterLab.
-->

---

<!-- _class: lab -->

## 🧪 À vous : atelier d'installation (30 min)

Suivez le notebook **`S01_lab_enonce.ipynb`**, partie 1, ou la fiche ci-dessous :

```bash
# 1. Vérifier Python (3.12 ou plus)
python --version              # Linux/macOS : python3 --version
# 2. Créer le projet et son venv
mkdir gestparc && cd gestparc
python -m venv .venv
# 3. Activer le venv
source .venv/bin/activate     # Windows : .venv\Scripts\activate
# 4. Installer JupyterLab
python -m pip install jupyterlab
# 5. Lancer le contrôle d'installation
python check_install.py
```

<!--
Timing : 30 min.
Circuler dans la salle. Problèmes fréquents :
- Windows : "Add python.exe to PATH" non coché → relancer l'installeur, option Modify.
- PowerShell refuse Activate.ps1 → Set-ExecutionPolicy -Scope CurrentUser RemoteSigned.
- Ubuntu/Debian : module venv absent → sudo apt install python3-venv.
- VS Code ne voit pas le venv → Ctrl+Shift+P, "Python: Select Interpreter".
- Proxy d'entreprise → pip install --proxy http://...
Objectif : 100 % des stagiaires avec check_install.py au vert avant la pause.
-->

---

## Instructions et exécution d'un script

Un script s'exécute **de haut en bas, une instruction par ligne**.

```python
# premier_script.py
print("Inventaire GestParc")
print("Nombre de postes :", 42)
print(10 + 32)
```

```text
$ python premier_script.py
Inventaire GestParc
Nombre de postes : 42
42
```

`print()` accepte plusieurs valeurs séparées par des virgules : elles sont affichées séparées par un espace.

<!--
Timing : 3 min.
Contrairement au REPL, un script n'affiche rien sans print().
Démo : exécuter le même fichier depuis le terminal puis avec le bouton ▶ de VS Code.
-->

---

## Les commentaires

```python
# Un commentaire commence par # et va jusqu'à la fin de la ligne
print("Démarrage")   # commentaire en fin de ligne

# Bon commentaire : il explique POURQUOI
# On garde 10 % de marge pour les mises à jour système.
reserved_gb = 50

# Mauvais commentaire : il répète le code
x = 50  # x vaut 50
```

Règle de la formation : **code et noms en anglais, commentaires en français**.

<!--
Timing : 2 min.
Les docstrings (""" ... """) seront vues en S5 avec les fonctions.
Raccourci VS Code : Ctrl+/ pour commenter ou décommenter une sélection.
-->

---

## Premières variables

Une variable est **un nom qui désigne une valeur**. On la crée par affectation avec `=`.

```python
hostname = "srv-web-01"
cpu_count = 8
ram_gb = 31.4
is_online = True

print(hostname, "a", cpu_count, "cœurs")
```

```text
srv-web-01 a 8 cœurs
```

Pas de déclaration de type : Python le déduit de la valeur (détails en S2).

<!--
Timing : 3 min.
Lire « hostname reçoit "srv-web-01" » et non « hostname égale ».
Ne pas entrer dans le détail des types (str, int, float, bool) : c'est le cœur de S2. Les nommer seulement si quelqu'un demande.
-->

---

## Python comme calculatrice

| Opérateur | Sens | Exemple | Résultat |
|---|---|---|---|
| `+` `-` `*` | addition, soustraction, multiplication | `8 * 4` | `32` |
| `/` | division (toujours décimale) | `7 / 2` | `3.5` |
| `//` | division entière | `7 // 2` | `3` |
| `%` | reste (modulo) | `7 % 2` | `1` |
| `**` | puissance | `2 ** 10` | `1024` |

```python
total_gb = 512
used_gb = 389
free_gb = total_gb - used_gb      # 123
```

<!--
Timing : 3 min.
Les autres opérateurs (comparaison, logiques, appartenance, identité) sont vus en S3.
Question : « Combien de minutes dans 135 secondes ? » → 135 // 60 = 2 min, 135 % 60 = 15 s.
-->

---

## Nommer ses variables

| ✅ Correct | ❌ Incorrect | Pourquoi |
|---|---|---|
| `server_count` | `2nd_server` | Ne commence pas par un chiffre |
| `disk_usage` | `disk-usage` | `-` est l'opérateur de soustraction |
| `vat_rate` | `class` | Mot réservé du langage |
| `ticket_id` | `t` | Nom non explicite |

- Convention **snake_case** : minuscules et `_`
- Python **distingue les majuscules** : `Total` et `total` sont deux variables
- Constantes en MAJUSCULES par convention : `APP_NAME = "GestParc"`

<!--
Timing : 2 min.
La convention PEP 8 complète sera vue en S14 ; on prend dès maintenant les bonnes habitudes.
-->

---

## Pièges fréquents de la première soirée

```python
>>> print "Bonjour"
SyntaxError: Missing parentheses in call to 'print'. Did you mean print(...)?

>>> print(nb_servers)
NameError: name 'nb_servers' is not defined

>>> Hostname = "srv-01"
>>> print(hostname)
NameError: name 'hostname' is not defined. Did you mean: 'Hostname'?
```

💡 **Lire le message d'erreur en partant de la dernière ligne** : type de l'erreur + explication.

<!--
Timing : 3 min.
Dédramatiser les erreurs : Python 3.12+ donne des suggestions très utiles ("Did you mean...").
Les exceptions seront traitées en profondeur en S10.
-->

---

<!-- _class: lab -->

## 🧪 À vous : Lab partie 2 + projet fil rouge (30 min)

Notebook **`S01_lab_enonce.ipynb`**, parties 2 et 3

- Exercices ⭐ à ⭐⭐⭐ : variables, calculs, nommage, lecture d'erreurs
- Exercice de synthèse : estimer la durée d'analyse d'un fichier de logs
- **GestParc – étape 0** : dossier projet, venv, `README.md`, `main.py` qui affiche la bannière de l'application

Les cellules `assert` vérifient vos réponses : **aucun message = c'est juste**.

<!--
Timing : 30 min.
Les rapides : section « Pour aller plus loin » (import this, help, documentation).
Ceux en difficulté : indices dans les blocs <details>.
Vérifier que chacun a bien le dossier gestparc/ avec main.py qui s'exécute : c'est le point de départ de toutes les étapes suivantes.
-->

---

## Récapitulatif

- Python 3 uniquement : Python 2 est en fin de vie depuis 2020
- REPL pour tester, **script `.py`** pour les programmes, **notebook** pour explorer
- Un **venv par projet** : `python -m venv .venv` puis activation
- `print()` affiche, `#` commente, `=` affecte une valeur à un nom
- Noms en snake_case, explicites, en anglais

**Pour la prochaine fois** (optionnel) : lire les sections 1 à 3 du tutoriel officiel sur docs.python.org/fr/3/

**Séance 2** : types, séquences, dictionnaires, références et mutabilité

<!--
Timing : 5 min.
Vérifier que chacun repart avec son venv fonctionnel et le dossier gestparc/.
Annoncer le quiz flash de début de S2 (5 questions sur S1).
-->
