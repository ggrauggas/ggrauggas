# Guia Git i GitHub — Exercicis pas a pas

---

## 1.1 Creació i actualització de repositoris

### Exercici 1 — Configurar Git
```bash
git config --global user.name "El teu Nom"
git config --global user.email "correu@exemple.com"
git config --global color.ui auto

# Mostrar la configuració
git config --list
```

---

### Exercici 2 — Crear repositori
```bash
mkdir llibre
cd llibre
git init

# Mostrar contingut
ls -la
```

---

### Exercici 3 — Primer fitxer i zona d'intercanvi
```bash
# Comprovar estat
git status

# Crear fitxer
cat > index.txt << 'EOF'
Capítol 1: Introducció a Git
Capítol 2: Flux de treball bàsic
Capítol 3: Repositoris remots
EOF

# Comprovar estat
git status

# Afegir a la zona d'intercanvi temporal (staging)
git add index.txt

# Comprovar estat
git status
```

---

### Exercici 4 — Primer commit
```bash
git commit -m "Afegit índex del llibre"
git status
```

---

### Exercici 5 — Modificar i fer commit
```bash
cat > index.txt << 'EOF'
Capítol 1: Introducció a Git
Capítol 2: Flux de treball bàsic
Capítol 3: Gestió de branques
Capítol 4: Repositoris remots
EOF

# Mostrar canvis respecte a l'última versió
git diff index.txt

git commit -am "Afegit capítol 3 sobre gestió de branques"
```

---

### Exercici 6 — Canviar missatge de commit
```bash
# Mostrar canvis de l'última versió respecte a l'anterior
git show

# Canviar missatge de l'últim commit
git commit --amend -m "Afegit capítol 3 sobre gestió de branques a l'índex"

# Tornar a mostrar els últims canvis
git show
```

---

## 1.2 Historial de canvis

### Exercici 1 — Historial i capítol 1
```bash
# Veure historial
git log

# Crear carpeta i fitxer
mkdir capitols
echo "Git és un sistema de control de versions ideat per Linus Torvalds" > capitols/capitol1.txt

git add capitols/capitol1.txt
git commit -m "Afegit capítol 1"

git log
```

---

### Exercici 2 — Capítol 2 i diferències
```bash
cat > capitols/capitol2.txt << 'EOF'
El flux de treball bàsic amb Git consistix en:
1- Fer canvis en el repositori.
2- Afegir els canvis a la zona d'intercanvi temporal.
3- Fer un commit dels canvis.
EOF

git add capitols/capitol2.txt
git commit -m "Afegit capítol 2"

# Diferències entre l'última versió i dues versions anteriors
git diff HEAD~2 HEAD
```

---

### Exercici 3 — Capítol 3 i diferències amb la primera versió
```bash
cat > capitols/capitol3.txt << 'EOF'
Git permet la creació de branques el que permet tindre diferents
versions del mateix projecte i treballar de manera simultània en elles.
EOF

git add capitols/capitol3.txt
git commit -m "Afegit capítol 3"

# Diferències entre la primera i l'última versió
git diff $(git rev-list --max-parents=0 HEAD) HEAD
```

---

### Exercici 4 — Annotació amb blame
```bash
echo "Capítol 5: Conceptes avançats" >> index.txt

git add index.txt
git commit -m "Afegit capítol 5 a l'índex"

# Veure qui ha fet canvis al fitxer
git blame index.txt
```

---

## 1.3 Desfer canvis

### Exercici 1 — Desfer canvis sense staging
```bash
# Eliminar l'última línia
head -n -1 index.txt > tmp.txt && mv tmp.txt index.txt

git status

# Desfer canvis (tornar a la versió anterior)
git checkout -- index.txt

git status
```

---

### Exercici 2 — Treure de staging i desfer
```bash
head -n -1 index.txt > tmp.txt && mv tmp.txt index.txt

git add index.txt
git status

# Treure de staging (manté els canvis al directori de treball)
git reset HEAD index.txt
git status

# Desfer els canvis al fitxer
git checkout -- index.txt
git status
```

---

### Exercici 3 — Múltiples canvis: treure de staging i desfer tot
```bash
# 1. Eliminar última línia d'index.txt
head -n -1 index.txt > tmp.txt && mv tmp.txt index.txt

# 2. Eliminar capitol3.txt
rm capitols/capitol3.txt

# 3. Crear capitol4.txt buit
touch capitols/capitol4.txt

git add .
git status

# Treure tots els canvis de staging
git reset HEAD .
git status

# Desfer tots els canvis (torna a la versió del repositori)
git checkout -- .
git clean -fd   # elimina fitxers nous no rastreats (capitol4.txt)
git status
```

---

### Exercici 4 — Desfer commits
```bash
# 1. Modificacions i commit accidental
head -n -1 index.txt > tmp.txt && mv tmp.txt index.txt
rm capitols/capitol3.txt
git add .
git commit -m "Esborrat accidental"

git log

# Desfer l'últim commit però mantindre els canvis (soft reset)
git reset --soft HEAD~1
git log
git status

# Tornar a fer el commit
git commit -m "Esborrat accidental"

# Desfer l'últim commit I els canvis al directori de treball (hard reset)
git reset --hard HEAD~1
git log
git status
```

---

## 1.4 Gestió de branques

### Exercici 1 — Crear branca
```bash
git branch bibliografia
git branch
```

---

### Exercici 2 — Commit a master
```bash
cat > capitols/capitol4.txt << 'EOF'
En este capítol veurem com usar GitHub per a allotjar repositoris en remot.
EOF

git add capitols/capitol4.txt
git commit -m "Afegit capítol 4"

# Historial amb totes les branques
git log --oneline --all --graph
```

---

### Exercici 3 — Treballar a la branca bibliografia
```bash
git checkout bibliografia

echo "Chacon, S. and Straub, B. Pro Git. Apress." > bibliografia.txt

git add bibliografia.txt
git commit -m "Afegida primera referència bibliogràfica"

git log --oneline --all --graph
```

---

### Exercici 4 — Fusionar i eliminar branca
```bash
git checkout master
git merge bibliografia

git log --oneline --all --graph

git branch -d bibliografia

git log --oneline --all --graph
```

---

### Exercici 5 — Conflicte i resolució
```bash
# Crear i canviar a bibliografia
git branch bibliografia
git checkout bibliografia

cat > bibliografia.txt << 'EOF'
Scott Chacon and Ben Straub. Pro Git. Apress.
Ryan Hodson. Ry's Git Tutorial. Smashwords (2014)
EOF

git add bibliografia.txt
git commit -m "Afegida nova referència bibliogràfica"

# Canviar a master i fer canvi conflictiu
git checkout master

cat > bibliografia.txt << 'EOF'
Chacon, S. and Straub, B. Pro Git. Apress.
Loeliger, J. and McCullough, M. Version control with Git. O'Reilly
EOF

git add bibliografia.txt
git commit -m "Afegida nova referència bibliogràfica"

# Fusionar (generarà conflicte)
git merge bibliografia

# Editar el fitxer i deixar-lo així:
cat > bibliografia.txt << 'EOF'
Chacon, S. and Straub, B. Pro Git. Apress.
Loeliger, J. and McCullough, M. Version control with Git. O'Reilly
Hodson, R. Ry's Git Tutorial. Smashwords (2014)
EOF

git add bibliografia.txt
git commit -m "Resolt conflicte de bibliografia"

git log --oneline --all --graph
```

---

## 1.5 Repositoris remots

### Exercici 1 — Connectar amb GitHub
```bash
# (Crear el repositori "llibre-git" manualment a github.com)

# Afegir el remot
git remote add origin https://github.com/usuari/llibre-git.git

# Mostrar remots configurats
git remote -v
```

---

### Exercici 2 — Pujar canvis
```bash
git push -u origin master

# Comprovar a github.com → repositori → historial de commits
```

---

### Exercici 3 — Col·laborar en repositori d'un altre usuari
```bash
# Clonar el repositori d'un company
git clone https://github.com/altreUsuari/llibre-git.git
cd llibre-git

# Crear fitxer autors
echo "Nom Cognom - correu@exemple.com" > autors.txt

git add autors.txt
git commit -m "Afegit autor"
git push
```

---

### Exercici 4 — Fork, branca autoria i pull request
```bash
# 1. Fer fork de asalber/llibre-git des de github.com

# 2. Clonar el fork
git clone https://github.com/usuari/llibre-git.git
cd llibre-git

# 3. Crear i activar branca autoria
git checkout -b autoria

# 4. Afegir dades al fitxer autors
echo "Nom Cognom - correu@exemple.com" >> autors.txt

git add autors.txt
git commit -m "Afegit nou autor"

# 5. Pujar la branca al remot
git push origin autoria

# 6. Fer el Pull Request des de github.com:
#    Repositori → "Compare & pull request" → Crear PR
```

---

## Resum de comandos clau

| Acció | Comando |
|---|---|
| Configurar usuari | `git config --global user.name "Nom"` |
| Iniciar repositori | `git init` |
| Veure estat | `git status` |
| Afegir a staging | `git add <fitxer>` o `git add .` |
| Fer commit | `git commit -m "missatge"` |
| Veure historial | `git log --oneline --all --graph` |
| Veure diferències | `git diff` |
| Desfer canvis (fitxer) | `git checkout -- <fitxer>` |
| Treure de staging | `git reset HEAD <fitxer>` |
| Desfer commit (soft) | `git reset --soft HEAD~1` |
| Desfer commit (hard) | `git reset --hard HEAD~1` |
| Crear branca | `git branch <nom>` |
| Canviar branca | `git checkout <nom>` |
| Fusionar branca | `git merge <nom>` |
| Eliminar branca | `git branch -d <nom>` |
| Afegir remot | `git remote add origin <url>` |
| Pujar canvis | `git push -u origin master` |
| Clonar repositori | `git clone <url>` |
