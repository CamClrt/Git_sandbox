## Git Sanbox

1. Forkez ce dépôt depuis votre GitHub pour créer son propre bac à sable.

Vous pouvez récupérer le projet en local à l'aide de la commande `git clone` et du lien que vous trouverez dans l'interface de votre dépôt distant fraichement forké en utilisant le menu vert "Code"

````
$ git clone https://github.com/mon_compte_github/Git_sandbox.git
````


2. Avant de démarrer, bien observer la structure du projet :

👉 l’ensemble des fichiers du dépôt  
👉 les éventuelles branches  
👉 l’ensemble des commits de chaque branche

3. Vérifier que tout est ok

```
$ git branch -v
```

3 bis. Si seule `main` est visible, visualiser les possibles autres branches du dépôt distant

```
$ git branch -a
```

3 ter. Récupérer `pingu_dev_branch`, observer la liste de vos branches et se replacer sur `main`

```
$ git checkout -b pingu_dev_branch origin/pingu_dev_branch
# Dans cas, il est aussi possibile de faire : git switch -c pingu_dev_branch
$ git branch -a
$ git checkout main
$ git branch -a
```
⚠️ A ce moment précis le dépôt vient juste d'être cloné, il est donc à jour par rapport au dépôt distant, sinon penser à faire un `git fetch` juste avant afin de mettre à jour le dépôt local par rapport au dépôt distant.

4. Créer une branche depuis son `main` local

```
$ git checkout -b cam_dev_branch
```

5. Créer une branche depuis le `main` distant

```
$ git checkout -b cam_dev_branch_bis origin/main
```

5 bis. Vérifier que tout est ok

```
$ git branch -av
```

6. Confirmer l’essai

- Créer une troisième branche de dev en local depuis `pingu_dev_branch` (step 4)

👉 ici il faudra utiliser la commande `checkout` pour se déplacer sur `pingu_dev_branch` puis `checkout -b`

- Créer une quatrième branche de dev en local depuis la branche `pingu_dev_branch` distante (step 5)

7. Pusher cette branche sur le dépôt distant

```
$ git push
```

💬 ici Git devrait être bavard, il indiquera que pour `push` la branche courante, l'utilisateur doit d’abord configurer l’upstream, c'est-à-dire le lien entre le dépôt local & le dépôt distant. 

Pour ce faire, suivre ses éventuelles suggestions :

```
$ git push --set-upstream origin ma_branche_courante
```

8. Supprimer cette quatrième branche de dev en local

```
$ git branch -D cam_dev_branch_quater
```

👉 Pour supprimer une branche, l'utilisateur ne peux pas rester sur la cible à détruire. Penser à se déplacer sur n’importe quelle autre branche avec `checkout`.

9. Supprimer aussi la branche distante

```
$ git push origin --delete cam_dev_branch_ter
```

⚠️ **ATTENTION** ⚠️ cette manipulation est lourde de conséquence, elle est à vérifier plusieurs fois avant de la confirmer.

Vous pouvez aussi faire de même pour la troisième branche de dev, tant en local qu'en distant.

10. Se placer sur la seconde branche de dev, ajouter un fichier `cool.py`, jeter un œil au résultat

```
$ git checkout cam_dev_branch_bis
$ touch cool.py
$ git status
$ git log
```

11. Ajouter ce fichier dans le suivi Git (stage), jeter un oeil au résultat

```
$ git add cool.py
$ git log
$ git status
```

12. Ajouter ce fichier au dépôt local en réalisant un commit, jeter un oeil au résultat

```
$ git commit -m "[ADD]: my first cool Python feature"
$ git status
$ git log
```

![lien d'illsutration](https://res.cloudinary.com/practicaldev/image/fetch/s--Si7ksd-d--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AdiRLm1S5hkVoh5qeArND0Q.png)

illustration: [source](https://res.cloudinary.com/practicaldev/image/fetch/s--Si7ksd-d--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AdiRLm1S5hkVoh5qeArND0Q.png)

13. Depuis GitHub faire une `pull request` entre votre branche de dev bis et votre branche de dev principale

⚠️ ATTENTION ⚠️ cela suppose que 2 branches de dev, la principale et la secondaire (bis) distantes existent et soient à jour. Pour ce faire pensez à `push` comme dans l'étape 7

13 bis. Valider votre `pull request`

Dans ce cas précis, la branche bis est en avance d'un commit sur la branche principale. Elle vient juste ajouter un fichier complémentaire à la branche de dev principale, le fichier `cool.py`. La review et relativement simple, il n'y a pas de source de conflit potentiel et les branches n'ont pas divergé.

👉 Pour plus d'informations sur les `pull requests` vous pouvez vous référer à cet [article](https://blog.mergify.com/what-is-a-pull-request/) et plus largement à ce [blog](https://blog.mergify.com/) 📚

14. Suite à cette validation, mettre à jour son dépôt local et plus précisément sa branch de dev principale et vérifier qu'elle a bien avancé d'un nouveau commit

```
$ git checkout cam_dev_branch
$ git pull origin cam_dev_branch
$ git log
```

15. Supprimer la branche de dev bis et visualiser les branches du dépôt local

```
$ git branch -D cam_dev_branch_bis
$ git branch -v
```

16. Placer vous sur la branche `pingu_dev_branch` et visualiser son contenu

```
$ git checkout pingu_dev_branch
$ git log
```

👉 Cette branche a comme base la branche `main` elle ne comporte donc pas le commit comprenant la création du fichier `cool.py` actuellement présent sur la branch de dev.

👉 En revanche, cette branche contient 2 commits d'avance, l'un apportant une correction sur de la typo, l'autre en proposant un nouveau tri de la liste contenue dans le fichier file1.

👉 En l'état la branche de dev principale ainsi que la branche `pingu_dev_branch` ont divergé. Pour envisager d'effectuer une `pull request`de l'ensemble de ces modifications vers notre `main`, par exemple, il faut d'abord mettre à jour notre branche de développement principale, c'est à dire intercaler les 2 commits de différences présents dans `pingu_dev_branch`.

17. Mettre à jour la branche de dev principale avec les modifications de `pingu_dev_branch`

```
$ git checkout cam_dev_branch
$ git log
$ git rebase pingu_dev_branch
$ git log
```

👉 Votre branche a intégré les modifications de `pingu_dev_branch` sans conflit, bravo !

18. Votre CTO a mis en place une protection sur les branches `main`, `dev` et `tests`. En l'état personne ne peut `push` ou `push --force` sur ces branches, ouf 😮  

Pour que vos contributions puissent être apportées au projet global vous devez ici soumettre vos `pull requests`sur la branche de `tests` puis une fois les tests validés ce code basculera sur la branche de `dev` puis la `main`. On appelle cela un `workflow`. Celui décrit ici est relativement simple. Chaque structure opte pour le `workflow` adapté à ses besoins.

Ici, si vous observer l'ensemble de vos branches à l'aide de `git branch -v` vous remarquerez que `main`, `dev`et `tests` ne sont pas au même niveau. Ils n'ont pas le même dernier commit. `dev` et `tests` ont un commit d'avance sur `main`.

Si vous vous souvenez de nos précédentes manipulations, nous avons créé plusieurs branches sur la base de `main` comme pour la branche de développement.

Afin le soumettre notre `pull request` sur la branche de test, il peut être bienvenu de mettre à jour notre branche courante. Cela permettrait notamment de s'assurer que l'ensemble de notre travail est toujours compatible avec les avancements déjà apportés à la codebase.

Pour ce faire nous allons nous placer sur cette branche et effectuer un rebase sur `dev`, bref les mêmes commandes que dans le point 17 😏.

💡 Avant cela, pensez à récupérer la branche `dev` en local, comme à l'étape 3

```
$ git checkout cam_dev_branch
$ git log
$ git rebase dev
```

19. et là, c’est le drame… 😱

```
Auto-merging src/file1
CONFLICT (content): Merge conflict in src/file1
error: could not apply f85fc78... [IMP]: reorder content
Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply f85fc78... [IMP]: reorder content
```

Votre invite de commande préférée indique que vous allez devoir mouiller le T-shirt & résoudre du conflit 😶 car Git, votre nouveau meilleur ami n’a pas réussi à s’en occuper seul. Mince alors, Linus qu’est-ce qu’il se passe ?!?

Concrètement, Git nous indique que ça bloque à cause du commit `f85fc78... [IMP]: reorder content`.

En effet, sur la branche `dev` le fichier file1 contient la liste des films Star Wars ordonnée dans un sens, alors que notre branche de dev courante, elle, fait état de la même liste dans le sens inverse.

Alors que faire ? 🤔 Indiquer à Git quelle version du code garder.

Nous partirons du principe que la réorganisation de la liste fait partie intégrante des modifications que nous souhaitons apporter. Une fois votre sélection faite à l’aide de votre éditeur de texte préféré, il est temps d’intégrer ces modifications :

```
$ git status
👉 prendre le temps de lire ce que Git a à dire

$ git rebase --continue

Ici, un éditeur de texte s’ouvre et vous propose de mettre à jour le message de commit concerné, à votre convenance.
Ne changez rien, enregistrez et hop hop, vous venez de résoudre ce conflit avec classe ! Bravo 👏
```

20. WIP, utiliser `git rebase -i` pour cleaner ses branches avant de les `push`, comment aller chercher un commit à la volée avec `cherry-pick`, c'est quoi un `merge`, pourquoi on n'est pas toujours obligé d'en faire & quelles sont les alternatives et avantages... #teaser 🍿

