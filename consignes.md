## Git Sanbox

1. Créer son propre bac à sable ou récupérer le projet en local

```
$ git clone https://github.com/CamClrt/Git_sandbox.git
```

2. Avant de démarrer, bien observer la structure du projet

👉 l’ensemble des fichier du main  
👉 les éventuelles branches  
👉 l’ensemble des commits de chaque branche  

3. Créer une branche depuis son `main` local

```
$ git checkout -b cam_dev_branch
```

4. Vérifier que tout est ok 
```
$ git branch
```

4 bis. Si seul `main` est visible, visualiser les possibles autres branches du dépôt distant

```
$ git branch -a
```

4 ter. Récupérer `pingu_dev_branch`

```
$ git switch -c pingu_dev_branch
```
⚠️ A ce moment précis le dépôt vient juste d'être cloné, il est donc à jour par rapport au dépôt distant. Si cette commande est utilisée à un tout autre moment, penser à faire un `git fetch` juste avant afin de mettre à jour le dépôt local par rapport au dépôt distant.

5. Créer une branche depuis le `main` distant

```
$ git checkout -b cam_dev_branch_bis origin/main
```

5 bis. Vérifier que tout est ok

```
$ git branch -av
```

6. Confirmer l’essai

- Créer une seconde branche depuis la branche de dev locale en local (step 4)
- Créer une troisième branche depuis la branche de dev distante en local (step 5)

7. Pusher cette branche sur le dépôt distant

```
$ git push
```

💬 ici Git sera bavard, il indiquera que pour `push` cette branche courante l'utilisateur doit d’abord configurer l’upstream, c'est-à-dire le lien entre le dépôt local & le dépôt distant. 

Pour ce faire, suivre ses précieuses suggestions:

```
$ git push --set-upstream origin ma_branche_courante
```

8. Supprimer cette troisième branche de dev en local

```
$ git branch -D cam_dev_branch_ter
```

👉 Pour supprimer une branche, l'utilisateur ne peux pas rester sur celle à détruire. Penser à se déplacer sur n’importe quelle autre branche.

```
$ git checkout l_elu_de_ton_choix
```

9. Supprimer aussi la branche distante

```
$ git push origin --delete cam_dev_branch_ter
```

⚠️ **ATTENTION** ⚠️ cette manipulation est lourde de conséquence, elle est à vérifier plusieurs fois avant de la confirmer.


