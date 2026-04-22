# ACT1 — Comandos Git i GitHub
**Gerard Grau Gascón**

---

## Configuració prèvia (executa una sola vegada)

```bash
git config --global user.name "Gerard Grau"
git config --global user.email "gerardgrau2004@gmail.com"
```

---

## 1.1 Repositori DEAW

**Pas manual:** Ves a github.com, crea un repositori nou anomenat `DEAW` (públic).

```bash
git clone https://github.com/gerardgrau2004/DEAW.git
cd DEAW
```

---

## 1.2 README

```powershell
Set-Content Readme.md "# DEAW`nRepositori per als exercicis del mòdul de Desplegament d'Aplicacions Web (DAW)."
```

---

## 1.3 Commit inicial

```bash
git add Readme.md
git commit -m "Comencem amb els exercicis de Git"
```

---

## 1.4 Push inicial

```bash
git push -u origin main
```

> Si el repositori usa `master` en lloc de `main`, substitueix `main` per `master` en tots els comandos.

---

## 1.5 Ignorar arxius

```powershell
ni privat.txt
mkdir privada
Add-Content .gitignore "privat.txt"
Add-Content .gitignore "privada/"
git add .gitignore
git commit -m "Afegim .gitignore amb privat.txt i privada/"
git push
```

---

## 1.6 Afegir fitxer 1.txt

```powershell
ni 1.txt
git add 1.txt
git commit -m "Afegim fitxer 1.txt"
git push
```

---

## 1.7 Crear el tag v0.1

```bash
git tag v0.1
```

---

## 1.8 Pujar el tag v0.1

```bash
git push origin v0.1
```

---

## 1.9 Compte de GitHub

**Passos manuals a github.com:**
- Ves a Settings > Profile i afegeix una foto.
- Ves a Settings > Password and authentication i activa el 2FA.

---

## 1.10 Ús social de GitHub

**Passos manuals a github.com:**
- Busca 2 companys de classe i segueix-los (botó Follow al seu perfil).
- Entra als seus repositoris DEAW i segueix-los (Watch > All Activity).
- Afegeix una estrela als seus repositoris DEAW (botó Star).

---

## 1.11 Crear una taula

Edita `Readme.md` i afegeix al final la taula següent (substitueix amb els noms reals):

```markdown
| NOMBRE          | GITHUB                              |
|-----------------|-------------------------------------|
| Nom company 1   | [usuari1](https://github.com/usuari1) |
| Nom company 2   | [usuari2](https://github.com/usuari2) |
| Nom company 3   | [usuari3](https://github.com/usuari3) |
```

```bash
git add Readme.md
git commit -m "Afegim taula de companys al Readme"
git push
```

---

## 1.12 Col·laboradors

**Pas manual a github.com:**
- Ves al repositori DEAW > Settings > Collaborators > Add people.
- Afegeix l'usuari `guivifra`.

---

## 1.13 Crear una branca v0.2

```bash
git checkout -b v0.2
```

---

## 1.14 Afegir fitxer 2.txt

```powershell
ni 2.txt
git add 2.txt
git commit -m "Afegim fitxer 2.txt en branca v0.2"
```

---

## 1.15 Crear branca remota v0.2

```bash
git push -u origin v0.2
```

---

## 1.16 Merge directe

```bash
git checkout main
git merge v0.2
git push
```

---

## 1.17 Merge amb conflicte

```powershell
# En master: escriure "Hola" a 1.txt
git checkout main
Set-Content 1.txt "Hola"
git add 1.txt
git commit -m "Afegim Hola a 1.txt en main"

# En v0.2: escriure "Adeu" a 1.txt
git checkout v0.2
Set-Content 1.txt "Adeu"
git add 1.txt
git commit -m "Afegim Adeu a 1.txt en v0.2"

# Tornar a main i fer merge (generarà conflicte)
git checkout main
git merge v0.2
```

---

## 1.18 Llistat de branques

```bash
git branch --merged
git branch --no-merged
```

---

## 1.19 Arreglar conflicte

Obre `1.txt` i edita'l manualment per resoldre el conflicte (elimina les marques `<<<<<<`, `=======`, `>>>>>>>`). Deixa el contingut definitiu que vulguis.

```bash
git add 1.txt
git commit -m "Resolem conflicte entre main i v0.2"
git push
```

---

## 1.20 Esborrar branca

```bash
git tag v0.2
git push origin v0.2
git branch -d v0.2
git push origin --delete v0.2
```

---

## 1.21 Llistat de canvis

```bash
git log --oneline --graph --all --decorate
```
