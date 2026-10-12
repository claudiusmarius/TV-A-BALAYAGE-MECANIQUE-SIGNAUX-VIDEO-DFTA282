# TV-A-BALAYAGE-MECANIQUE-SIGNAUX-VIDEO-DFTA282
Signaux vidéos

# Mechanical TV - Mise en Forme des Signaux Vidéo (NBTV 32 lignes)

Ce dépôt héberge les fichiers de conception, les schémas et les simulations relatifs au module de traitement analogique des signaux pour mon moniteur de **Télévision Mécanique (NBTV)** fonctionnant au standard international de 32 lignes et 12,5 images par seconde.

L'objectif de cette révision  est de requalifier le PCB d'origine afin de résoudre les conflits d'impédances et les pertes de synchronisation sur les images animées analogiques.

## 🛠️ Spécifications Techniques & Architecture

Le schéma est architecturé autour d'un quadruple amplificateur opérationnel **LM324** (alimenté en *Single Supply* +15V / GND) et balaie le signal de gauche à droite :

* **U2.A (Étage d'Entrée) :** Tampon suiveur associé à une structure d'entrée haute impédance (1 MΩ / 470 kΩ) pour isoler la source vidéo et éviter tout écrêtage.
* **U2.B (DC Restorer actif) :** Circuit de clampage calé sur une tension de **Talon artificielle d'environ 2V** au point **TP8**. Cette structure éloigne le signal de la zone de saturation basse de l'AOP (\(V_{OL}\) spécifié à 20mV max) pour garantir un fonctionnement purement linéaire. La résistance **R42 (470 kΩ)** fait office de résistance de fuite pour assurer le suivi dynamique des variations de luminosité.
* **Q5 (Isolation) :** Transistor NPN 2N2222 monté en émetteur-suiveur agissant comme un écran total pour ne pas charger la boucle du DC Restorer.
* **U2.C (Séparateur de Synchro) :** Configurateur en **Trigger de Schmitt** à rétroaction positive (R₄₁ = 100 kΩ). Le calcul des seuils intègre la tension réelle de saturation haute du LM324 et l'impédance de fuite de **R12 (47 kΩ)** vers le point B.
* **U2.D (Rabotage des Noirs) :** Soustracteur unitaire pur chargé de supprimer les puits de synchro du signal utile envoyé vers la matrice de LED (*LED Arrays*). L'ajustement prend en compte le décalage naturel de 0,7V (VBE) introduit par Q5.
* **Q8 / Q9 (Double Générateur de Courant) :** Paire de transistors PNP 2N2907 fournissant deux courants constants indépendants d'environ 300 μA pour verrouiller et stabiliser ratiométriquement les seuils du Talon (TP8) et du rabotage (TP9).

## 📁 Contenu du Dépôt

* `/Schematics` : Fichiers sources et exports PDF du schéma définitif **EasyEDA**.
* `/Simulation` : Fichiers de simulation **LTspice** (.asc) pour la validation des points de fonctionnement statiques et dynamiques.

## 📺 Vidéo de Présentation

L'explication détaillée de ce circuit, la méthode de modification pas à pas du PCB et les essais de qualification sur table sont présentés dans cette vidéo YouTube : https://youtu.be/yAubQpv7da0


---
*Remerciements particuliers à Chris (UK) et Peter Spies (NL) de la communauté internationale NBTVA pour leur support technique et leurs analyses croisées.*
