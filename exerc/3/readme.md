cd 3
git checkout -b e3-deleteme
touch a b c d e f g h i
git add a && git commit -m'Delete-me-1'
git add b && git commit -m'Delete-me-2'
git add c && git commit -m'Delete-me-3'
git add d && git commit -m'Save-me-1'
git add e && git commit -m'Delete-me-4'
git add f && git commit -m'Save-me-2'
git add g && git commit -m'Save-me-3'
git add h && git commit -m'Delete-me-5'
git add i && git commit -m'Save-me-4'


**Ejercicio 3:** 
1. Cambia a la rama e3-deleteme
2. Copia los commits Save-me-X a la rama e3-saved
3. Borra la rama e3-deleteme
4. Verifica que en e3-saved solo están los commits Save-me-X
```bash
$ git cherry-pick [commits]
$ git branch -D <branch>
```
