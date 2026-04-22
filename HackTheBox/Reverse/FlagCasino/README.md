# Challenge : FlagCasino
**Plateforme :** HackTheBox  
**Catégorie :** Reverse Engineering  
**Difficulté :** Easy  
**Flag :** `HTB{r4nd_1s_v3ry_pr3d1ct4bl3}`

## Description
> The team stumbles into a long-abandoned casino.
 As you enter, the lights and music whir to life, and a staff of robots begin moving around 
and offering games, while skeletons of prewar patrons are slumped at slot machines.
 A robotic dealer waves you over and promises great wealth if you can win -
 can you beat the house and gather funds for the mission?

> L'équipe découvre par hasard un casino abandonné depuis longtemps. 
À peine entrés, les lumières et la musique s'animent,
et une armée de robots se met à s'affairer, proposant des jeux, 
tandis que les squelettes d'anciens clients d'avant-guerre sont affalés devant les machines à sous.
Un croupier robotisé vous fait signe de vous approcher et vous promet une fortune si vous gagnez.
 Parviendrez-vous à battre le casino et à réunir les fonds nécessaires à la mission ?


## Analyse
### Décompilation avec Binary Ninja
Le binaire lit un caractère, applique `srand(char)` 
puis compare `rand()` avec un tableau `check[]`.

### Vulnérabilité identifiée
`srand/rand` est déterministe → inversible par bruteforce.

## Solution
1. Construire le mapping inverse `rand() → chr(i)`
2. Lire les 29 valeurs de `check[]` dans le binaire
3. Retrouver chaque caractère

## Script
\```python
import ctypes
from pwn import *
...
\```

## Leçons apprises
- `rand()` n'est pas aléatoire si la seed est prévisible
- pwntools permet de lire les symboles d'un binaire