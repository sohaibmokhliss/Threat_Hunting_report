# Rapport de Threat Hunting - Projet LaTeX

Rapport académique et professionnel complet sur un projet de Threat Hunting réalisé au sein de DataProtect.

## 📋 Description

Ce rapport documente un projet de simulation d'attaque et d'investigation sur un environnement Windows, en utilisant la méthode ACH (Analysis of Competing Hypotheses) pour analyser et reconstituer une chaîne d'attaque complète.

### Thème du rapport

**Threat Hunting : Détection d'un Brute Force Réussi suivi d'une Exfiltration de Données**

## 🏗️ Structure du projet

```
threat-hunting-report/
│
├── main.tex                          # Fichier principal LaTeX
├── preamble.tex                      # Configuration et packages LaTeX
│
├── frontmatter/                      # Pages préliminaires
│   ├── cover.tex                     # Page de couverture
│   ├── abstract.tex                  # Résumés FR/EN
│   ├── acknowledgements.tex          # Dédicaces et remerciements
│   └── acronyms.tex                  # Liste des abréviations
│
├── chapters/                         # Chapitres du rapport
│   ├── introduction.tex              # Introduction générale
│   ├── chapitre1_contexte.tex        # Contexte (DataProtect, Jobintech)
│   ├── chapitre2_environnement.tex   # Environnement technique
│   ├── chapitre3_threat_hunting.tex  # Théorie Threat Hunting et ACH
│   ├── chapitre4_simulation_attaque.tex    # Simulation de l'attaque
│   ├── chapitre5_investigation_ach.tex     # Investigation ACH (CENTRAL)
│   ├── chapitre6_resultats_impact.tex      # Résultats et recommandations
│   ├── chapitre7_perspectives.tex          # Perspectives futures
│   └── conclusion.tex                      # Conclusion générale
│
├── bibliography/
│   └── references.bib                # Bibliographie BibTeX
│
├── figures/                          # Dossier pour les images
│   └── README.md                     # Instructions pour les figures
│
└── context/                          # Fichiers source et images
    ├── Images PNG (logos, captures d'écran)
    └── Fichiers texte de contexte
```

## 📚 Contenu des chapitres

### Chapitre 1 - Contexte général du projet
- Présentation de DataProtect et Jobintech
- Problématique et objectifs du projet
- Gestion et planification

### Chapitre 2 - Environnement technique
- Machines virtuelles (Windows Server, Kali Linux)
- Outils utilisés (Elastic Security, Sysmon, Impacket)
- Framework MITRE ATT&CK

### Chapitre 3 - Threat Hunting en cybersécurité
- Fondements du Threat Hunting
- Méthode ACH (Analysis of Competing Hypotheses)
- Les 8 étapes de l'ACH

### Chapitre 4 - Simulation de l'attaque
- AS-REP Roasting avec Impacket
- Craquage hors-ligne avec John The Ripper
- PowerShell encodé pour reconnaissance
- Accès RDP avec credentials compromis
- Création de tâches planifiées malveillantes
- Exfiltration via BITS

### Chapitre 5 - Investigation ACH (CHAPITRE CENTRAL)
- Formulation de 4 hypothèses (H1-H4)
- Documentation de 15 preuves (P1-P15)
- Matrice ACH complète
- Élimination raisonnée des hypothèses
- Conclusion formelle d'incident
- Requêtes SIEM utilisées

### Chapitre 6 - Résultats et recommandations
- Synthèse des résultats
- Évaluation de l'impact
- Recommandations stratégiques
- Nouveaux cas d'usage SIEM

### Chapitre 7 - Perspectives futures
- Élargissement du périmètre des attaques
- Automatisation et orchestration (SOAR)
- Intelligence artificielle et machine learning
- Programme Purple Team

## 🛠️ Compilation

### Prérequis

- Distribution LaTeX complète (TeX Live, MiKTeX, ou MacTeX)
- Packages requis : geometry, graphicx, hyperref, fancyhdr, setspace, booktabs, longtable, acronym, float, listings, biblatex

### Commandes de compilation

#### Avec Biber (recommandé)

```bash
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

#### Avec BibTeX

```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

#### Avec latexmk (automatique)

```bash
latexmk -pdf main.tex
```

## 📊 Caractéristiques techniques

- **Classe de document** : `report` (12pt, A4)
- **Langue** : Français (avec abstract en anglais)
- **Interligne** : 1.5
- **Style de code** : Listings avec coloration syntaxique
- **Tables** : booktabs pour un style professionnel
- **Références** : BibLaTeX avec style numérique

## 🎯 Points clés du rapport

### Techniques d'attaque simulées

- **T1558.004** - AS-REP Roasting (Credential Access)
- **T1059.001** - PowerShell (Execution)
- **T1053.005** - Scheduled Task/Job (Persistence)
- **T1027** - Obfuscated Files or Information (Defense Evasion)
- **T1197** - BITS Jobs (Exfiltration)
- **T1083** - File and Directory Discovery
- **T1087** - Account Discovery

### Méthode ACH appliquée

La méthode ACH (Analysis of Competing Hypotheses) est au cœur de l'investigation :
1. Identification de 4 hypothèses concurrentes
2. Collecte de 15 preuves documentées
3. Matrice de confrontation systématique
4. Élimination des hypothèses incohérentes
5. Conclusion avec niveau de confiance (95%)

## 👥 Auteurs

- Mme LABIED Chayma
- Mr GHRISSE Oussama  
- Mr Jaber Oussama

**Encadrant** : M. ABDELBARY EBady (DataProtect)

**Organisme d'accueil** : DataProtect  
**Organisme de financement** : Jobintech

**Période** : Du 11 Décembre 2025 au 02 janvier 2026  
**Année universitaire** : 2025/2026

## 📝 Licence

Ce rapport académique est fourni à des fins éducatives et professionnelles.

## 🔗 Références principales

- MITRE ATT&CK Framework
- Elastic Security Documentation
- Analysis of Competing Hypotheses (Heuer, 1999)
- DataProtect - Expertise en cybersécurité

## 📧 Contact

Pour toute question concernant ce rapport :
- DataProtect : [www.dataprotect.ma](https://www.dataprotect.ma)

---

**Note** : Ce projet démontre l'efficacité d'une approche structurée du Threat Hunting combinant simulation d'attaque réaliste et analyse méthodique pour détecter des compromissions sophistiquées.
