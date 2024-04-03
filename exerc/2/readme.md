**Ejercicio 2:** 
1. Genera tres nuevos archivo con algún contenido y commitealo
2. Modifica el contenido de los tres archivos (deben quedar en workdir)
3. Agrega uno de los tres archivos a index
4. Genera un nuevo archivo y agregalo a index
5. Genera un archivo sin seguimiento de git
- En este punto debes tener dos archivos en workdir, dos archivos en index y un archivo sin seguimiento -
6. Genera una entrada en stash con ambos archivos en index con el mensaje "Stash 1 index <archivo1 archivo2>"
7. Genera un segundo stash con ambos archivo en work dir con el mensaje "Stash 2 workdir <archivo3 archivo4>"
8. Genera un stash con el archivo sin seguimiento
9. Lista los archivos de ambos stash
10. Modifica el contenido de cualquiera de los tres archivos generados en el paso 1
11. Recupera el contenido de ambos stash
12. ¿Ambos stash se pudieron recuperar sin problema?
13. Commitea todos los archivos

```bash
$ git stash list
$ git stash push -m"message" -- file1 file2 
$ git stash show <n>
$ git stash pop <n>
```
