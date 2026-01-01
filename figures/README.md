# Instructions pour les figures

Ce dossier doit contenir les images référencées dans le rapport LaTeX.

## Figures disponibles dans context/

Les figures suivantes sont disponibles dans le dossier `context/` et sont déjà référencées dans les chapitres :

### Chapitre 1 - Contexte général du projet

1. **DataProtect_is_the_company_responsible_for_delivering_the_training_program_providing_the_technical_instruction_and_practical_learning_content.png**
   - Description : Logo de l'entreprise DataProtect
   - Référence LaTeX : `\ref{fig:dataprotect-logo}`
   - Utilisé dans : `chapitre1_contexte.tex`

2. **Jobintech_is_the_organization_that_fully_funds_the_training_program_enabling_participants_to_attend_the_formation_free_of_charge.png**
   - Description : Logo Jobintech - Organisme de financement
   - Référence LaTeX : `\ref{fig:jobintech}`
   - Utilisé dans : `chapitre1_contexte.tex`

### Chapitre 4 - Simulation de l'attaque

3. **AS-REP Roasting Attack.png**
   - Description : Capture d'écran de l'attaque AS-REP Roasting avec Impacket
   - Référence LaTeX : `\ref{fig:asrep-roasting}`
   - Utilisé dans : `chapitre4_simulation_attaque.tex`

4. **Offline Password Cracking with Jhon The Reaper.png**
   - Description : Craquage hors-ligne du mot de passe avec John The Ripper
   - Référence LaTeX : `\ref{fig:password-cracking}`
   - Utilisé dans : `chapitre4_simulation_attaque.tex`

5. **Access to the machine victim via RDP.png**
   - Description : Accès à la machine victime via RDP
   - Référence LaTeX : `\ref{fig:rdp-access}`
   - Utilisé dans : `chapitre4_simulation_attaque.tex`

## Format des images

- **Format recommandé** : PNG (pour les captures d'écran) ou PDF (pour les diagrammes vectoriels)
- **Résolution** : 300 DPI minimum pour les captures d'écran
- **Taille** : Optimiser pour réduire la taille du fichier sans perdre en qualité

## Comment ajouter de nouvelles figures

1. Placer l'image dans ce dossier (`figures/`)
2. Dans le fichier LaTeX du chapitre concerné, utiliser :

```latex
\begin{figure}[H]
\centering
\includegraphics[width=0.8\textwidth]{figures/nom-du-fichier.png}
\caption{Description de la figure}
\label{fig:reference-unique}
\end{figure}
```

3. Référencer la figure dans le texte avec : `comme illustré dans la figure \ref{fig:reference-unique}`

## Figures additionnelles recommandées

Pour enrichir le rapport, vous pourriez ajouter :

- Diagramme d'architecture du projet
- Diagramme de Gantt du planning
- Captures d'écran de l'interface Elastic Security
- Captures d'écran de Kibana avec les requêtes SIEM
- Schémas explicatifs des techniques d'attaque
- Captures d'écran de Sysmon configuré
- Timeline visuelle de l'attaque
- Graphiques des métriques de détection

## Notes importantes

- Les chemins des images dans `context/` sont référencés directement depuis la racine : `context/nom-fichier.png`
- Pour les images dans ce dossier `figures/`, utiliser : `figures/nom-fichier.png`
- Vérifier que toutes les images référencées existent avant de compiler le document
- Les images avec des espaces dans le nom de fichier peuvent poser problème, utiliser des tirets ou underscores

## Compilation LaTeX

Pour compiler le document avec les figures :

```bash
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

Ou si vous utilisez BibTeX au lieu de Biber :

```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```
