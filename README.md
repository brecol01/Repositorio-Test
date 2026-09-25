# 🧠 Chuleta de Git

Guía rápida con los comandos básicos de **Git** y **GitHub**, explicados de forma simple para consultarla cuando se me olvide algo.

---

## 🗺️ Cómo funciona Git en 30 segundos

```
Carpeta de trabajo  ──git add──▶  Staging  ──git commit──▶  Repositorio local  ──git push──▶  GitHub
   (tus archivos)              (preparados)                (historial guardado)               (la nube)
```

- **Commit**: una "foto" de tu proyecto en un momento concreto.
- **Rama (branch)**: una línea de trabajo paralela, para probar cosas sin romper `main`.
- **Remoto (`origin`)**: la copia del repositorio que vive en GitHub.

---

## ⚙️ 1. Configuración inicial (una sola vez)

| Comando | Qué hace |
|---|---|
| `git config --global user.name "Tu Nombre"` | Nombre que aparece en tus commits |
| `git config --global user.email "tu@correo.com"` | Correo asociado a tus commits |
| `git config --global init.defaultBranch main` | Las ramas nuevas se llamarán `main` |
| `git config --list` | Ver toda la configuración |

---

## 🚀 2. Empezar un proyecto

| Comando | Qué hace |
|---|---|
| `git init` | Convierte la carpeta actual en un repositorio |
| `git clone <url>` | Descarga un repositorio de GitHub a tu equipo |
| `git remote add origin <url>` | Conecta tu repo local con uno de GitHub |
| `git remote -v` | Muestra a qué remotos estás conectado |

---

## 🔄 3. Flujo del día a día

```bash
git status                       # 1. Ver qué ha cambiado
git add .                        # 2. Preparar todos los cambios
git commit -m "Qué he cambiado"  # 3. Guardar la foto con un mensaje
git push                         # 4. Subir a GitHub
```

| Comando | Qué hace |
|---|---|
| `git status` | Muestra archivos modificados y preparados. **Úsalo siempre** |
| `git add <archivo>` | Prepara solo un archivo |
| `git add .` | Prepara todos los cambios |
| `git commit -m "mensaje"` | Guarda los cambios preparados |
| `git push` | Sube tus commits a GitHub |
| `git pull` | Descarga y une los cambios de GitHub |

> 💡 **Regla de oro:** haz `git pull` antes de empezar a trabajar y `git push` al terminar.

---

## 🔍 4. Ver qué ha pasado

| Comando | Qué hace |
|---|---|
| `git log --oneline` | Historial de commits, una línea por commit |
| `git log --oneline --graph --all` | Historial con dibujo de ramas |
| `git diff` | Cambios que aún no has preparado |
| `git diff --staged` | Cambios ya preparados para el commit |
| `git show` | Detalle del último commit |

---

## 🌿 5. Ramas (branches)

| Comando | Qué hace |
|---|---|
| `git branch` | Lista las ramas (la actual lleva `*`) |
| `git switch -c nombre-rama` | Crea una rama nueva y te cambia a ella |
| `git switch nombre-rama` | Cambia a una rama existente |
| `git branch -d nombre-rama` | Borra una rama (ya fusionada) |
| `git push -u origin nombre-rama` | Sube una rama nueva a GitHub |

> 💡 Truco: `git push -u origin HEAD` sube la rama actual sin escribir su nombre.

---

## 🔀 6. Merge: unir ramas

**Merge** trae los cambios de una rama a otra. Siempre te colocas en la rama que **recibe** los cambios.

Ejemplo: quiero llevar mi rama `mi-rama` a `main`:

```bash
git switch main          # 1. Me pongo en la rama que recibe (main)
git pull                 # 2. La actualizo con lo de GitHub
git merge mi-rama        # 3. Traigo los cambios de mi-rama
git push                 # 4. Subo el resultado a GitHub
git branch -d mi-rama    # 5. (Opcional) Borro la rama ya unida
```

### ⚠️ Si hay conflicto

Ocurre cuando dos ramas cambiaron **las mismas líneas** de un archivo. Git te avisa y marca el archivo así:

```
<<<<<<< HEAD
Versión de la rama actual
=======
Versión de la otra rama
>>>>>>> mi-rama
```

Cómo resolverlo:

1. Abre el archivo y deja solo el texto correcto (borra las marcas `<<<<<<<`, `=======`, `>>>>>>>`).
2. Guarda el archivo.
3. Termina la fusión:

```bash
git add .
git commit -m "Resuelvo conflicto"
```

Si te asustas y quieres cancelar el merge: `git merge --abort`.

> 💡 **Alternativa en GitHub:** sube la rama, pulsa **Compare & pull request** y luego **Merge**. Es lo mismo pero desde la web.

---

## ⏪ 7. Deshacer errores

| Situación | Comando |
|---|---|
| Quiero descartar los cambios de un archivo (¡no se recuperan!) | `git restore <archivo>` |
| Preparé un archivo con `add` y me arrepiento | `git restore --staged <archivo>` |
| Me equivoqué en el mensaje del último commit (aún sin push) | `git commit --amend -m "Nuevo mensaje"` |
| Deshacer un commit ya subido, sin borrar historial | `git revert <id-del-commit>` |
| Guardar cambios a medias para más tarde | `git stash` |
| Recuperar lo guardado con stash | `git stash pop` |

---

## 🚫 8. Ignorar archivos (`.gitignore`)

Crea un archivo llamado `.gitignore` con los nombres que Git debe ignorar:

```
.DS_Store
*.log
node_modules/
.env
```

---

## 🆘 9. Errores típicos

| Error | Causa y solución |
|---|---|
| `fatal: no es un repositorio git` | Estás fuera de la carpeta del repo. Haz `cd` a ella |
| `rejected ... fetch first` / `non-fast-forward` | GitHub tiene cambios que tú no. Haz `git pull` y luego `git push` |
| `no tiene una rama upstream` | Usa `git push --set-upstream origin nombre-rama` |
| `nothing to commit` | No hay cambios. Guarda los archivos y revisa con `git status` |
| `src refspec ... no concuerda` | Escribiste mal el nombre de la rama, o aún no hay ningún commit |

---

## 📌 Chuleta ultra-rápida

```bash
git status                  # ¿qué pasa?
git add . && git commit -m "mensaje"   # guardar
git push                    # subir
git pull                    # bajar
git switch -c rama          # nueva rama
git merge rama              # unir rama a la actual
git log --oneline           # historial
```