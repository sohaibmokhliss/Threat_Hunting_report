# Guide de Compilation du Rapport LaTeX

Ce document explique comment compiler le rapport de Threat Hunting au format PDF.

## Prérequis

### Installation de LaTeX

#### Windows

Installez **MiKTeX** :
1. Téléchargez depuis https://miktex.org/download
2. Exécutez l'installateur
3. Choisissez "Install missing packages on-the-fly: Yes"

Ou installez **TeX Live** :
1. Téléchargez depuis https://tug.org/texlive/acquire-netinstall.html
2. Exécutez install-tl-windows.exe

#### macOS

Installez **MacTeX** :
```bash
brew install --cask mactex
```

Ou téléchargez depuis https://tug.org/mactex/

#### Linux (Ubuntu/Debian)

```bash
sudo apt-get update
sudo apt-get install texlive-full
sudo apt-get install texlive-lang-french
sudo apt-get install biber
```

#### Linux (Fedora/RHEL)

```bash
sudo dnf install texlive-scheme-full
```

### Vérifier l'installation

```bash
pdflatex --version
biber --version
```

## Méthodes de compilation

### Méthode 1 : Compilation manuelle (recommandée)

```bash
cd /path/to/Threat_Hunting_report
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

**Explication :**
- 1ère compilation : Génère les fichiers auxiliaires et références
- Biber : Traite la bibliographie
- 2ème compilation : Intègre la bibliographie
- 3ème compilation : Finalise les références croisées

### Méthode 2 : Avec latexmk (automatique)

```bash
latexmk -pdf main.tex
```

Latexmk détecte automatiquement le nombre de compilations nécessaires.

### Méthode 3 : Si vous n'avez que BibTeX (pas Biber)

Modifiez `preamble.tex`, ligne bibliographie :
```latex
% Remplacez cette ligne :
\usepackage[style=numeric, sorting=none]{biblatex}

% Par :
\usepackage[backend=bibtex,style=numeric]{biblatex}
```

Puis compilez :
```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

## Nettoyage des fichiers temporaires

### Linux/macOS

```bash
rm -f *.aux *.log *.out *.toc *.lof *.lot *.fls *.fdb_latexmk *.synctex.gz *.bbl *.blg *.bcf *.run.xml
```

### Windows (PowerShell)

```powershell
Remove-Item *.aux, *.log, *.out, *.toc, *.lof, *.lot, *.fls, *.fdb_latexmk, *.synctex.gz, *.bbl, *.blg, *.bcf, *.run.xml
```

### Avec latexmk

```bash
latexmk -c  # Nettoie les fichiers temporaires
latexmk -C  # Nettoie tout, y compris le PDF
```

## Résolution de problèmes courants

### Erreur : "File not found"

**Problème :** LaTeX ne trouve pas un fichier inclus.

**Solution :**
- Vérifiez que tous les fichiers .tex sont présents dans les dossiers chapters/, frontmatter/
- Vérifiez que les images PNG sont dans le dossier context/

### Erreur : "Undefined control sequence"

**Problème :** Commande LaTeX non reconnue.

**Solution :**
- Installez les packages manquants
- Sur MiKTeX, activez l'installation automatique des packages
- Sur TeX Live, installez texlive-full

### Erreur : "Package babel Error: Unknown language 'french'"

**Solution :**
```bash
# Ubuntu/Debian
sudo apt-get install texlive-lang-french

# Fedora
sudo dnf install texlive-babel-french
```

### Erreur bibliographie : "Empty bibliography"

**Solution :**
- Vérifiez que references.bib existe dans bibliography/
- Utilisez biber au lieu de bibtex
- Si biber ne fonctionne pas, changez pour backend=bibtex dans preamble.tex

### Warning : "Citation undefined"

**Solution :** C'est normal après la première compilation. Exécutez biber puis recompilez 2 fois.

### Problème : Images ne s'affichent pas

**Solution :**
- Vérifiez que les images PNG existent dans context/
- Les noms de fichiers avec espaces peuvent poser problème
- Les chemins sont relatifs depuis main.tex

## Édition du document

### Éditeurs LaTeX recommandés

#### TeXstudio (Multi-plateforme)
- Interface intuitive avec aperçu
- Auto-complétion
- Vérification orthographique
- Téléchargement : https://www.texstudio.org/

#### Overleaf (En ligne)
- Pas d'installation nécessaire
- Collaboration en temps réel
- Compilateur intégré
- Site : https://www.overleaf.com/

#### Visual Studio Code
Avec extensions :
- LaTeX Workshop
- LaTeX Utilities

#### TeXmaker (Multi-plateforme)
- Léger et rapide
- Téléchargement : https://www.xm1math.net/texmaker/

### Workflow de travail recommandé

1. **Éditer** un fichier .tex dans chapters/ ou frontmatter/
2. **Sauvegarder** les modifications
3. **Compiler** avec la commande appropriée
4. **Vérifier** le PDF généré
5. **Corriger** les erreurs si nécessaire
6. **Répéter** le processus

## Structure des fichiers

```
main.tex                    # Point d'entrée principal (NE PAS MODIFIER l'ordre des includes)
preamble.tex                # Configuration LaTeX (packages, styles)
├── frontmatter/            # Pages préliminaires
│   ├── cover.tex
│   ├── acknowledgements.tex
│   ├── abstract.tex
│   └── acronyms.tex
├── chapters/               # Contenu principal
│   ├── introduction.tex
│   ├── chapitre1_contexte.tex
│   ├── ...
│   └── conclusion.tex
├── bibliography/
│   └── references.bib      # Références bibliographiques
└── figures/                # Images additionnelles
```

## Personnalisation

### Changer la taille de police

Dans `main.tex`, ligne 1 :
```latex
\documentclass[14pt,a4paper]{report}  % Au lieu de 12pt
```

### Changer les marges

Dans `preamble.tex`, section geometry :
```latex
\usepackage[a4paper, top=3cm, bottom=3cm, left=3.5cm, right=3cm]{geometry}
```

### Changer l'interligne

Dans `preamble.tex` :
```latex
\doublespacing  % Au lieu de \onehalfspacing (1.5)
```

### Ajouter votre logo

1. Placez votre logo dans figures/
2. Dans `frontmatter/cover.tex`, remplacez :
```latex
\textit{(Logo DataProtect)}
```
Par :
```latex
\includegraphics[width=5cm]{figures/logo-dataprotect.png}
```

## Compilation en ligne de commande avancée

### Compiler avec arrêt sur erreur

```bash
pdflatex -halt-on-error main.tex
```

### Mode batch (non-interactif)

```bash
pdflatex -interaction=batchmode main.tex
```

### Spécifier un répertoire de sortie

```bash
pdflatex -output-directory=build main.tex
```

## Conversion vers d'autres formats

### LaTeX vers Word

```bash
pandoc main.tex -o rapport.docx
```

Note : La conversion peut perdre certains formatages complexes.

### LaTeX vers HTML

```bash
htlatex main.tex
```

## Support et ressources

### Documentation LaTeX

- **LaTeX Wikibook** : https://en.wikibooks.org/wiki/LaTeX
- **Overleaf Learn** : https://www.overleaf.com/learn
- **CTAN** : https://www.ctan.org/ (packages LaTeX)

### Aide communautaire

- **TeX Stack Exchange** : https://tex.stackexchange.com/
- **LaTeX subreddit** : https://www.reddit.com/r/LaTeX/

### Vérification de syntaxe en ligne

- **Overleaf** : Importez votre projet pour vérifier la compilation
- **Papeeria** : https://papeeria.com/

## Checklist avant compilation finale

- [ ] Tous les fichiers .tex sont présents
- [ ] Toutes les images référencées existent
- [ ] La bibliographie (references.bib) est complète
- [ ] Aucune TODO ou note personnelle dans le texte
- [ ] Les noms d'auteurs et dates sont corrects
- [ ] Vérification orthographique effectuée
- [ ] Compilation réussie sans erreur
- [ ] Table des matières correcte
- [ ] Liste des figures/tableaux correcte
- [ ] Toutes les références croisées fonctionnent
- [ ] La bibliographie s'affiche correctement

## Commandes de compilation complètes

### Workflow complet

```bash
# 1. Nettoyer les anciens fichiers
latexmk -C

# 2. Première compilation
pdflatex main.tex

# 3. Traiter la bibliographie
biber main

# 4. Deuxième compilation (intègre la biblio)
pdflatex main.tex

# 5. Troisième compilation (références croisées)
pdflatex main.tex

# 6. Vérifier le PDF
# Le fichier main.pdf devrait être généré
```

### Script bash de compilation automatique

Créez un fichier `compile.sh` :

```bash
#!/bin/bash
echo "=== Compilation du rapport de Threat Hunting ==="
echo "Étape 1/4 : Première compilation..."
pdflatex -interaction=nonstopmode main.tex > /dev/null

echo "Étape 2/4 : Traitement de la bibliographie..."
biber main > /dev/null

echo "Étape 3/4 : Deuxième compilation..."
pdflatex -interaction=nonstopmode main.tex > /dev/null

echo "Étape 4/4 : Finalisation..."
pdflatex -interaction=nonstopmode main.tex > /dev/null

echo "=== Compilation terminée ==="
echo "Le rapport est disponible : main.pdf"
```

Rendez-le exécutable et lancez-le :
```bash
chmod +x compile.sh
./compile.sh
```

### Script PowerShell (Windows)

Créez un fichier `compile.ps1` :

```powershell
Write-Host "=== Compilation du rapport de Threat Hunting ===" -ForegroundColor Green
Write-Host "Étape 1/4 : Première compilation..."
pdflatex -interaction=nonstopmode main.tex | Out-Null

Write-Host "Étape 2/4 : Traitement de la bibliographie..."
biber main | Out-Null

Write-Host "Étape 3/4 : Deuxième compilation..."
pdflatex -interaction=nonstopmode main.tex | Out-Null

Write-Host "Étape 4/4 : Finalisation..."
pdflatex -interaction=nonstopmode main.tex | Out-Null

Write-Host "=== Compilation terminée ===" -ForegroundColor Green
Write-Host "Le rapport est disponible : main.pdf"
```

Exécutez-le :
```powershell
.\compile.ps1
```

---

**Note finale :** Pour toute question ou problème, consultez les logs de compilation (main.log) qui contiennent des informations détaillées sur les erreurs éventuelles.
