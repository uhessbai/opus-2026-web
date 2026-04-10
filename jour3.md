# Jour 3 — Intelligence artificielle & apprendre à apprendre

## Comment fonctionne un LLM (en pratique)

Un LLM (Large Language Model) comme ChatGPT ou Claude est un modèle entraîné sur d'énormes quantités de texte. Il prédit le mot le plus probable à chaque étape — c'est pour ça qu'il peut écrire, expliquer, coder, traduire.

### Les tokens

Quand vous écrivez à une IA, votre message est découpé en **tokens** — des morceaux de mots ou de caractères. La réponse aussi consomme des tokens. C'est l'unité de mesure de base : plus vous écrivez, plus vous en consommez.

### Le contexte

Chaque conversation est chargée en **contexte** : le modèle "voit" l'ensemble de l'échange depuis le début pour répondre. Ce qui veut dire :

> A chaque message envoyé, **toute la conversation depuis le début est renvoyée au modèle**. Plus la conversation est longue, plus la consommation de tokens est importante — et plus le modèle peut perdre en précision.

Un contexte saturé peut faire "oublier" les premières informations ou dégrader la qualité des réponses.

### Bonnes pratiques

- **Pas trop court, pas trop long** : une question vague donne une réponse vague ; une question noyée dans trop de détails aussi
- **Nouvelle conversation = nouveau sujet** : ne pas accumuler des sujets différents dans le même fil
- **Reprendre un sujet long** : si une conversation est trop chargée, en ouvrir une nouvelle en lui apportant le contexte essentiel (résumé, extrait, fichier)

---

## Ce qu'on peut faire avec une IA

- **Coder** : générer, corriger, expliquer du code
- **Rechercher et synthétiser** : résumer un document, trouver des informations, comparer des options
- **Créer** : textes, images, sons, vidéos
- **Automatiser** : créer des scripts ou des workflows répétitifs
- **Apprendre** : poser des questions, se faire expliquer, explorer un sujet progressivement

---

## Les grandes IA du moment

| Outil | Type | Points notables |
|---|---|---|
| **ChatGPT** (OpenAI) | Texte, image, code | Le plus connu, très généraliste |
| **Claude** (Anthropic) | Texte, code | Très orienté code, hallucine moins, moins généraliste |
| **Gemini** (Google) | Texte, image, code | Intégré à l'écosystème Google |
| **Mistral** | Texte, code | Français, open-source, performant et léger |
| **DeepSeek** | Texte, code | Chinois, très performant, modèle open-source |
| **Qwen** (Alibaba) | Texte, code | Chinois, multilingue, en forte progression |
| **Midjourney** | Image | Génération d'images, très haute qualité visuelle |
| **ElevenLabs** | Audio / voix | Clonage et synthèse vocale réaliste |

---

## Bonnes pratiques générales

- **Donner un rôle** : "Tu es un développeur senior, tu dois..." — le modèle adapte son niveau et son ton
- **Être précis dans la demande** : format attendu, longueur, public cible, contraintes
- **Passer des références** : coller un extrait de code, un texte, une liste — le modèle travaille mieux avec du concret
- **Choisir le bon outil** : image → Midjourney, voix → ElevenLabs, code → Claude, généraliste → ChatGPT ou Gemini
- **Itérer** : ne pas hésiter à corriger, préciser, demander autrement — c'est un dialogue
- **Vérifier** : une IA peut se tromper avec assurance. Toujours recouper les informations importantes

---

## Limites et vigilance

### Les hallucinations

C'est le point le plus important à garder en tête : **une IA peut inventer des informations avec la même assurance que quand elle a raison**. Elle ne "sait" pas qu'elle se trompe — elle prédit, elle ne vérifie pas.

Exemples courants : des dates fausses, des citations inventées, des liens qui n'existent pas, du code qui ne fonctionne pas.

> Règle de base : **toujours vérifier une information importante** auprès d'une source externe avant de l'utiliser ou de la transmettre.

### Ce que l'IA n'est pas

- Elle n'a pas de conscience, pas d'opinion réelle, pas d'intention
- Sa connaissance est **figée dans le temps** (elle ne sait pas ce qui s'est passé après sa date d'entraînement, sauf si elle a accès à internet)
- Elle reflète les **biais de ses données** d'entraînement — elle n'est pas neutre par défaut

### Confidentialité

Les conversations envoyées à une IA peuvent être utilisées pour améliorer les modèles ou lues par des équipes humaines selon les plateformes.

**Ne jamais partager :**
- Mots de passe ou identifiants
- Données personnelles sensibles (numéros, coordonnées bancaires...)
- Informations confidentielles professionnelles ou clients

En cas de doute : relire les conditions d'utilisation de la plateforme, ou utiliser un modèle en local.

### Crédit et éthique

Quand on utilise une IA pour produire du contenu — texte, image, code — la question se pose : qu'est-ce qui est "son" travail, et qu'est-ce qui est le tien ?

Il n'y a pas de réponse universelle, mais quelques repères :
- Mentionner l'usage de l'IA quand c'est pertinent (dans un contexte scolaire, professionnel ou créatif)
- Garder la main sur les décisions et le sens — l'IA exécute, c'est vous qui choisissez
- Le droit d'auteur autour des contenus générés par IA est encore flou légalement dans la plupart des pays

---

## Utiliser avec conscience

Explorer, tester, apprendre — c'est exactement ce que ces outils permettent. Mais comme tout outil, ça se mérite une utilisation réfléchie.

Chaque requête envoyée à un LLM consomme de l'énergie réelle : serveurs, refroidissement, électricité. On ne laisse pas sa moto tourner toute la nuit pour rien — avec l'IA c'est pareil. Ce n'est pas une raison de ne pas s'en servir, c'est une raison de **savoir pourquoi on s'en sert**.

Quelques questions simples à se poser avant de lancer une requête :
- Est-ce que j'ai vraiment besoin d'une IA pour ça, ou je peux le faire moi-même ?
- Est-ce que je vais apprendre quelque chose, ou juste déléguer ?
- Est-ce que le résultat va avoir du sens une fois produit ?

**Produire avec du sens**, c'est aussi ça l'enjeu de ces semaines.

---

## Apprendre à apprendre (métacognition)

L'IA est un outil puissant — mais l'objectif n'est pas de lui laisser tout faire. L'idée, c'est **d'apprendre grâce à son aide**.

La **métacognition**, c'est la capacité à réfléchir sur sa propre façon d'apprendre. C'est une compétence qui se développe et qui permet d'explorer n'importe quel sujet plus efficacement.

Quelques principes clés :

- **Faire des connexions** : relier ce qu'on découvre à ce qu'on sait déjà — c'est comme ça que les connaissances s'ancrent
- **Se poser des questions** : ne pas consommer passivement — "pourquoi ça marche comme ça ?", "comment je ferais autrement ?"
- **Alterner effort et repos** : le cerveau consolide pendant les pauses, pas pendant l'intensité. Respecter son rythme d'énergie
- **Espacer les révisions** : revoir un sujet à intervalles croissants est bien plus efficace que tout revoir d'un coup
- **Accepter de ne pas comprendre tout de suite** : la confusion est une étape normale, pas un échec
- **Enseigner ou reformuler** : expliquer ce qu'on vient d'apprendre, même à soi-même, révèle immédiatement ce qu'on n'a pas vraiment compris

> L'IA peut vous donner une réponse en 5 secondes. Mais c'est la question que vous posez — et ce que vous faites de la réponse — qui détermine ce que vous apprenez vraiment.
