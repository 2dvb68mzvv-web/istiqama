# Istiqama — Installation GitHub Pages

Application web autonome (PWA) : accueil, religion, habitudes, calendriers, bilans, données locales et sauvegardes manuelles. Aucun compte requis.

## Mettre en ligne gratuitement

1. Décompresse `Istiqama_GitHub_Pages.zip` sur ton ordinateur.
2. Connecte-toi à [github.com](https://github.com) et crée un **nouveau dépôt public**, par exemple `istiqama`.
3. Dans ce dépôt, choisis **Add file → Upload files**, puis envoie **le contenu du dossier** (les fichiers `index.html`, `app.js`, `style.css`, `mosque_times.json`, `sw.js`, `manifest.webmanifest` et le dossier `assets`). Ne place pas un dossier supplémentaire autour de ces fichiers.
4. Confirme avec **Commit changes**.
5. Ouvre **Settings → Pages → Build and deployment** : source **Deploy from a branch**, branche **main**, dossier **/(root)**, puis sauvegarde.
6. Une fois publié, le site aura une adresse proche de `https://TON-PSEUDO.github.io/istiqama/` (remplace TON-PSEUDO par ton véritable identifiant GitHub).
7. Ouvre l'adresse sur **Safari iPhone** → **Partager** → **Sur l'écran d'accueil**. Active **« Ouvrir comme app web »**, si ce choix apparaît.

La première ouverture du site nécessite Internet pour charger l'application. Les fichiers de l'application peuvent ensuite fonctionner hors connexion grâce au service worker, après mise en cache. L'application garde son historique sur **l'appareil et le navigateur utilisés** : un autre téléphone ou navigateur ne voit pas automatiquement les mêmes données.

## Sauvegarder ses données

Dans la roue dentée (Paramètres) :
- **Exporter JSON** pour récupérer la totalité des données. Déplace le fichier vers `Fichiers`, iCloud Drive ou un support de sauvegarde.
- **Restaurer JSON** pour réimporter les données : soit remplacer l'historique actuel, soit fusionner avec résolution des conflits.

Important : GitHub Pages héberge le code, **pas tes saisies personnelles**. Les données sont enregistrées dans `IndexedDB`, ou `localStorage` en secours. Safari/iOS peut supprimer des données locales, notamment si l'app est désinstallée ou les données de site effacées. Exporte régulièrement.

## Horaires de la mosquée

`mosque_times.json` contient **105 dates** transcrites de l'enregistrement MAWAQIT fourni : **01/11/2026**, puis **tous les jours du 17/11/2026 au 28/02/2027**. Les dates 02–16/11/2026 ne sont pas dans la source, et aucune valeur n'a été inventée.

Ces horaires ont été **extraits d'une vidéo** et **ne sont pas certifiés par la mosquée** : la mention « Extrait à vérifier » apparaît dans l'application. Les décalages `+10` et `+6` n'ont **pas** été transformés en heures d'iqama car leur signification n'a pas été confirmée. Les heures d'iqama ne s'affichent que si elles sont renseignées explicitement.

Il n'y a **aucun calcul automatique** pour les dates absentes. Tu peux importer plus tard d'autres horaires officiels fournis par ta mosquée, ou les saisir à la main dans Paramètres.

### Format des fichiers d'horaires

**CSV** (heures au format HH:MM) :

```csv
date,Fajr,Chourouk,Dhuhr,Asr,Maghrib,Isha,iqamaFajr,iqamaDhuhr,iqamaAsr,iqamaMaghrib,iqamaIsha
2027-03-01,06:00,07:30,12:45,16:00,18:30,20:00,,,,,
```

**JSON** :

```json
{
  "entries": {
    "2027-03-01": {
      "Fajr": "06:00",
      "Chourouk": "07:30",
      "Dhuhr": "12:45",
      "Asr": "16:00",
      "Maghrib": "18:30",
      "Isha": "20:00"
    }
  }
}
```

*Ces horaires d'exemple sont fictifs : ne les importe pas comme horaires réels.*

## Utilisation des suivis

- Religion : prières détaillées, Coran (711 pages par défaut), istighfar et dhikr séparés.
- Habitudes : siwak, huile de nigelle, fil dentaire et habitudes personnalisées.
- Calendriers : mensuel/annuel, un suivi ou tous les suivis. Cliquer sur un jour pour consulter l'historique et le modifier.
- Bilans : totaux, jours avec activité, moyennes sur les jours renseignés, graphiques, comparaisons de périodes et records.
- Une habitude sans saisie reste **« non renseignée »**. Elle n'est jamais marquée « non effectuée » automatiquement.

## Limites et précautions

- Cette V1 n'est pas un service de synchronisation : les données ne sont pas sauvegardées sur GitHub.
- L'import CSV nécessite des colonnes et heures bien formées.
- La ponctualité des prières est déclarée manuellement, sans décision automatique basée sur les heures.
- Pour la lecture du Coran, corriger une ancienne date ne modifie pas la position actuelle. Le bouton « Lecture terminée » enregistre une lecture complète et remet la position actuelle à zéro seulement si la date choisie est celle du jour.
- Le calcul des séries de jours porte sur les jours avec une activité **enregistrée**, pas sur l'assiduité religieuse réelle.

## Arborescence

```
index.html
app.js
style.css
mosque_times.json
manifest.webmanifest
sw.js
assets/
  icon-192.png
  icon-512.png
```

Toute la logique est autonome : aucune dépendance npm ni connexion à un fournisseur tiers.
