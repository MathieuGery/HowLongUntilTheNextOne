# How Long Until The Next One

Un compteur élégant qui affiche le temps restant jusqu'à une date cible définie par une variable d'environnement.

## Configuration

1. Installez les dépendances :
```bash
npm install
```

2. Configurez la date cible dans le fichier `.env` :
```
TARGET_DATE=2025-12-31T23:59:59
```

3. Démarrez le serveur de développement :
```bash
npm run dev
```

## Format de la date

La variable `TARGET_DATE` doit être au format ISO 8601 :
- `YYYY-MM-DDTHH:MM:SS` (exemple: `2025-12-31T23:59:59`)
- `YYYY-MM-DD` (exemple: `2025-12-31`)

## Scripts disponibles

- `npm run dev` - Démarre le serveur de développement
- `npm run build` - Construit l'application pour la production
- `npm run preview` - Prévisualise la version de production

## Fonctionnalités

- Compteur en temps réel (jours, heures, minutes, secondes)
- Design responsive et moderne
- Animation quand la date est atteinte
- Support du mode sombre/clair
- Configuration via variable d'environnement
