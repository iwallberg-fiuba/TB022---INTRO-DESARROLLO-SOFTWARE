<br><br>

### Table of Contents

<br>

[Colaborar usando Git y Github](#Colaborar-usando-Git-y-Github)

<br>

- [Explicado](#Explicado)
- [Pull Request (PR)](#Pull-Request-PR)
 - [Revisión](#Revisión)
 - [Merge de PR](#Merge-de-PR)
 - [Limpieza Posterior](#Limpieza-Posterior)

<br>

[Extra](#Extra)
- [Merge Conflicts](#Merge-Conflicts)
- [Issues](#Issues)

<br><br>

---

<br><br>


---

<br>

## Explicado

<br><br>



<br>

### Merge de PR

<br>

7. Una vez revisado el Pull Request por los demás integrantes, se selecciona:

<br>

```text
Merge Pull Request
```

<br>

GitHub combinará ambas ramas.

<br>

```text
main
 │
 ├── feature/login
 │       ↓
 │      Pull Request
 │       ↓
 │      Revisión
 │       ↓
 └──── Merge
```

<br>

Ahora los cambios ya forman parte de `main` en GitHub.

<br>
<br>
<br>

### Limpieza posterior

<br>

8. Después del merge GitHub suele mostrar:

<br>

```text
Pull Request merged successfully
↓
Delete branch
```

<br>

Esto elimina la rama en GitHub y hay que hacerlo.

<br><br>

9. Actualizar la copia local de main

<br>

```shell
git switch main
git pull
```

<br><br>

10. Eliminar la rama local porque ya no es necesaria (su contenido ya fue incorporado a `main`).

<br>

```shell
git branch -d feature/login
```

<br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br>

---

<br>

## Extra

<br><br>

### Merge Conflicts

<br>

| Paso | Acción                                                                           |
| ---- | -------------------------------------------------------------------------------- |
| 1    | Se crea un Pull Request                                                          |
| 2    | GitHub intenta combinar la rama origen con la rama destino                       |
| 3    | GitHub verifica si existen conflictos                                            |
| 4    | GitHub detecta que ambas ramas modificaron líneas incompatibles                  |
| 5    | GitHub informa que no es posible realizar el merge hasta resolver los conflictos |
| 6    | Se actualiza la rama local con los cambios más recientes de la rama destino      |
| 7    | Se ejecuta `git status` para identificar los archivos con conflictos             |
| 8    | Se editan manualmente los archivos y se resuelven los conflictos                 |
| 9    | Se ejecuta `git add .`                                                           |
| 10   | Se ejecuta `git commit -m "resolver conflictos"`                                 |
| 11   | Se ejecuta `git push`                                                            |
| 12   | GitHub vuelve a verificar el Pull Request                                        |
| 13   | Si ya no existen conflictos, GitHub habilita la opción de realizar el merge      |
| 14   | Se realiza manualmente el merge mediante el botón Merge Pull Request             |

<br><br><br>


