---
marp: true
theme: default
paginate: true
size: 16:9
header: 'Python – Programmation, approche objet et bonnes pratiques'
footer: 'S3 · Les structures de contrôle'
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
  section.quiz { background: #eef6ff; }
  section.quiz h2 { border-color: #1f4e78; }
  img[alt~="center"] { display: block; margin: 0 auto; }
  .cols { display: grid; grid-template-columns: 1fr 1fr; gap: 24px; }
---

<!-- _class: title -->
<!-- _paginate: false -->
<!-- _header: '' -->

# Séance 3
## Les structures de contrôle

**Objectifs de la séance**
- Structurer le code en blocs grâce à l'indentation
- Écrire des conditions avec `if` / `elif` / `else` et l'opérateur ternaire
- Utiliser tous les opérateurs : comparaison, logiques, appartenance, identité
- Répéter avec `while` et `for` (`range`, `enumerate`, `zip`)
- Contrôler les boucles : `break`, `continue`, `pass`, `else`

<!--
Timing : 1 min.
Fil conducteur : à la fin de la soirée, GestParc aura un vrai menu interactif.
-->

---

<!-- _class: quiz -->

## ⚡ Quiz flash : séance 2

1. Que vaut `"srv-web-01"[4:7]` ?
2. Que renvoie `type(input("Âge : "))` ?
3. Comment créer un ensemble vide ?
4. `a = [1, 2]`, `b = a`, `b.append(3)` : que vaut `a` ?
5. Écrire en une ligne l'échange des valeurs de `x` et `y`.

<!--
Timing : 10 min.
Réponses : 1. 'web' — 2. <class 'str'> — 3. set() (et non {}) — 4. [1, 2, 3], alias — 5. x, y = y, x
-->

---

## Plan de la séance

| Durée | Bloc |
|---|---|
| 10 min | Quiz flash |
| 20 min | Théorie 1 : indentation, conditions, opérateurs |
| 30 min | 🧪 Lab partie 1 |
| 5 min | Pause |
| 20 min | Théorie 2 : boucles `while` et `for`, branchements |
| 30 min | 🧪 Lab partie 2 + GestParc étape 2 : menu console |
| 5 min | Récapitulatif |

---

## L'indentation fait partie de la syntaxe

```python
disk_usage = 0.93
if disk_usage > 0.9:
    print("Disque presque plein")      # bloc du if
    print("Nettoyage des logs requis")  # même bloc
print("Contrôle terminé")              # hors du bloc
```

- Un bloc commence après `:` et est **indenté de 4 espaces** (PEP 8)
- Toutes les lignes d'un bloc ont la même indentation
- Les blocs s'imbriquent : 4 espaces de plus par niveau
- Ne jamais mélanger tabulations et espaces

<!--
Timing : 2 min.
Pas d'accolades ni de "end" : c'est l'indentation qui délimite.
IndentationError : montrer l'erreur en démo en décalant une ligne.
VS Code convertit Tab en 4 espaces par défaut.
-->

---

## `if` / `elif` / `else`

```python
disk_usage = 0.78

if disk_usage >= 0.9:
    level = "CRITICAL"
elif disk_usage >= 0.7:
    level = "WARNING"
else:
    level = "OK"

print(f"Disque à {disk_usage:.0%} : {level}")
```

```text
Disque à 78% : WARNING
```

Les conditions sont testées **dans l'ordre** : la première vraie l'emporte.

<!--
Timing : 3 min.
Question : que se passe-t-il si on inverse les deux premières conditions ? (une valeur de 0.95 serait classée WARNING).
Pas de switch historique : match/case existe depuis 3.10, on le cite seulement.
-->

---

## L'opérateur ternaire

```python
is_online = False
status = "en ligne" if is_online else "hors ligne"

ram_gb = 6
advice = "OK" if ram_gb >= 8 else "Mise à niveau conseillée"
print(status, "-", advice)
```

```text
hors ligne - Mise à niveau conseillée
```

`valeur_si_vrai if condition else valeur_si_faux`

💡 À réserver aux cas simples : sinon, un `if` classique est plus lisible.

---

## Opérateurs de comparaison

| Opérateur | Sens | Exemple | Résultat |
|---|---|---|---|
| `==` / `!=` | égal / différent | `"web" == "Web"` | `False` |
| `<` `<=` `>` `>=` | ordre | `"apple" < "banana"` | `True` |
| chaînage | encadrement | `0 <= port < 1024` | port système ? |

```python
port = 443
print(0 <= port < 1024, port == 443, "10" < "9")
```

```text
True True True
```

⚠️ Les chaînes se comparent caractère par caractère : `"10" < "9"`.

<!--
Timing : 2 min.
Le chaînage 0 <= port < 1024 est propre à Python et très lisible.
Piège des chaînes de chiffres : convertir en int avant de comparer.
-->

---

## Opérateurs logiques et valeurs « vraies »

| Opérateur | Vrai si… |
|---|---|
| `a and b` | les deux sont vrais |
| `a or b` | au moins un est vrai |
| `not a` | `a` est faux |

**Valeurs considérées comme fausses** : `False`, `None`, `0`, `0.0`, `""`, `[]`, `{}`, `set()`

```python
tickets = []
if not tickets:
    print("Aucun ticket ouvert")
```

Évaluation **paresseuse** : `user and user["name"]` ne lit pas la clé si `user` est vide.

<!--
Timing : 3 min.
« if tickets: » est l'idiome Python pour « la liste n'est pas vide ».
Priorité : not > and > or ; mettre des parenthèses en cas de doute.
-->

---

## Appartenance et identité

```python
ALLOWED_PORTS = {22, 80, 443}
port = 8080
print(port in ALLOWED_PORTS, port not in ALLOWED_PORTS)

laptop = {"asset_tag": "LT-001", "assigned_to": None}
print("brand" in laptop)              # cherche dans les CLÉS
if laptop["assigned_to"] is None:
    print("Équipement disponible")
```

```text
False True
False
Équipement disponible
```

- `in` : liste, tuple, str (sous-chaîne), set (rapide), dict (clés)
- `is` / `is not` : **même objet** ; à utiliser surtout avec `None`

<!--
Timing : 3 min.
Rappel S2 : on compare des valeurs avec ==, on teste None avec is.
"ERROR" in line : test de sous-chaîne, très utile pour les logs.
-->

---

<!-- _class: lab -->

## 🧪 À vous : Lab partie 1 (30 min)

Notebook **`S03_lab_enonce.ipynb`**, partie 1

- Ex. 1 ⭐ : niveau d'alerte d'un disque
- Ex. 2 ⭐ : statut avec l'opérateur ternaire
- Ex. 3 ⭐⭐ : politique de mots de passe
- Ex. 4 ⭐⭐ : règles de pare-feu (appartenance, identité)
- Ex. 5 ⭐⭐⭐ : priorité d'un ticket (conditions imbriquées)

---

## La boucle `while`

Répéter **tant qu'une condition est vraie**.

```python
attempts = 0
delay = 1
while attempts < 4:
    attempts += 1
    print(f"Tentative {attempts} : nouvel essai dans {delay} s")
    delay *= 2
```

```text
Tentative 1 : nouvel essai dans 1 s
Tentative 2 : nouvel essai dans 2 s
Tentative 3 : nouvel essai dans 4 s
Tentative 4 : nouvel essai dans 8 s
```

⚠️ La condition doit finir par devenir fausse : sinon, boucle infinie (Ctrl+C).

<!--
Timing : 3 min.
Opérateurs d'affectation composés : +=, -=, *=, //=...
Usage typique : menus, nouvelles tentatives, lecture jusqu'à une condition.
-->

---

## La boucle `for` et `range()`

Parcourir **chaque élément** d'une séquence.

```python
servers = ["srv-web-01", "srv-db-01", "srv-app-01"]
for server in servers:
    print("Sauvegarde de", server)

for i in range(3):           # 0, 1, 2
    print(i, end=" ")
print()
for port in range(8000, 8010, 3):
    print(port, end=" ")
```

```text
Sauvegarde de srv-web-01
Sauvegarde de srv-db-01
Sauvegarde de srv-app-01
0 1 2 
8000 8003 8006 8009
```

<!--
Timing : 3 min.
range(début, fin, pas) : fin exclue, comme le slicing.
for parcourt aussi une chaîne (caractère par caractère), un set, un dict (ses clés).
-->

---

## `enumerate()` et `zip()`

```python
servers = ["srv-web-01", "srv-db-01"]
loads = [0.42, 0.91]

for index, server in enumerate(servers, start=1):
    print(index, server)

for server, load in zip(servers, loads):
    print(f"{server}: {load:.0%}")
```

```text
1 srv-web-01
2 srv-db-01
srv-web-01: 42%
srv-db-01: 91%
```

<!--
Timing : 3 min.
enumerate : évite le compteur manuel et range(len(...)), qui est un anti-pattern en Python.
zip : parcourt plusieurs séquences en parallèle, s'arrête à la plus courte.
-->

---

## Parcourir un dictionnaire

```python
stock = {"laptop": 48, "server": 6, "printer": 9}

for category, count in stock.items():
    print(f"{category:<8} {count:>3}")

total = 0
for count in stock.values():
    total += count
print("Total :", total)
```

```text
laptop    48
server     6
printer    9
Total : 63
```

<!--
Timing : 2 min.
for key in d parcourt les clés ; d.values() les valeurs ; d.items() les couples (clé, valeur) avec unpacking.
Compter avec un dictionnaire : counts[k] = counts.get(k, 0) + 1 (utile dans l'ex. de synthèse).
-->

---

## `break`, `continue`, `pass`

```python
log_lines = ["# en-tête", "INFO start", "ERROR disk", "FATAL crash", "INFO end"]
for line in log_lines:
    if line.startswith("#"):
        continue            # ligne suivante
    if line.startswith("FATAL"):
        print("Arrêt de l'analyse :", line)
        break               # sortie de la boucle
    if line.startswith("INFO"):
        pass                # rien à faire (pour l'instant)
    else:
        print("À traiter :", line)
```

```text
À traiter : ERROR disk
Arrêt de l'analyse : FATAL crash
```

---

## `else` sur une boucle

Le bloc `else` s'exécute si la boucle se termine **sans `break`**.

```python
used_ips = {"10.0.0.10", "10.0.0.11", "10.0.0.13"}
for last_byte in range(10, 15):
    candidate = f"10.0.0.{last_byte}"
    if candidate not in used_ips:
        print("Première IP libre :", candidate)
        break
else:
    print("Aucune IP libre dans la plage")
```

```text
Première IP libre : 10.0.0.12
```

<!--
Timing : 2 min.
Lire le else comme « sinon, si on n'a rien trouvé ».
Pattern de recherche classique : for ... if trouvé: break ... else: pas trouvé.
-->

---

## Pièges fréquents

| Piège | Exemple | Correction |
|---|---|---|
| `=` au lieu de `==` | `if level = "OK":` | `if level == "OK":` |
| Oubli des `:` | `else` | `else:` |
| Boucle infinie | compteur jamais incrémenté | vérifier la progression |
| Modifier la liste parcourue | `for x in l: l.remove(x)` | parcourir une copie `l[:]` |
| `range(len(l))` | `for i in range(len(l)): l[i]` | `for x in l` ou `enumerate` |
| `or` mal utilisé | `if level == "ERROR" or "FATAL":` | `if level in ("ERROR", "FATAL"):` |

<!--
Timing : 2 min.
Le dernier piège est très fréquent : "FATAL" seul est toujours vrai (chaîne non vide).
-->

---

<!-- _class: lab -->

## 🧪 À vous : Lab partie 2 (30 min)

Notebook **`S03_lab_enonce.ipynb`**, parties 2 et 3

- Ex. 6 ⭐ : capacité totale d'un cluster (`for`)
- Ex. 7 ⭐⭐ : liste numérotée (`enumerate`)
- Ex. 8 ⭐⭐ : serveurs surchargés (`zip`)
- Ex. 9 ⭐⭐ : nouvelles tentatives avec attente croissante (`while`)
- Ex. 10 ⭐⭐⭐ : première IP libre (`break` / `else`)
- Synthèse : statistiques d'un journal d'événements
- **GestParc – étape 2** : menu console en boucle

---

## Récapitulatif

- Blocs délimités par `:` et l'**indentation** (4 espaces)
- `if` / `elif` / `else`, ternaire `a if cond else b`
- Opérateurs : comparaison (chaînables), `and` / `or` / `not`, `in`, `is None`
- `while` : tant que ; `for` : pour chaque élément
- `range`, `enumerate`, `zip`, `dict.items()`
- `break`, `continue`, `pass`, `else` de boucle

**Séance 4 (TP)** : algorithmes classiques et automates à états

<!--
Timing : 5 min.
Prévenir : S4 est un TP, prévoir d'être autonome, les algorithmes de S4 seront réécrits en fonctions en S5.
-->
