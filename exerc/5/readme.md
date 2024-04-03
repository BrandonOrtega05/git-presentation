**Ejercicio 5:** 
1. Genera tres commits
2. Deshaz el último commit (soft)
3. Deshaz los últimos dos commits (soft)
4. Vuelve a commitear los mismos cambios (deshechos) en un solo commit
```bash
$ git reset HEAD~
```


**Ejercicio 6:** 
1. Reutilizando el commit del ejercicio anterior, reviertelo
2. Verifica que se hayan revertido los cambios
```bash
$ git revert [commit] 
```
