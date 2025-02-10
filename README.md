# Systeme-de-Sauvegarde-Automatise-Recuperation
 Ce projet démontre comment automatiser la sauvegarde d’un dossier et comment restaurer les données en cas de besoin.
 ## 1. Objectifs du Projet

- **Automatisation de la sauvegarde :** Créer un script Bash qui compresse et sauvegarde un dossier source dans un répertoire de sauvegarde.
- **Planification automatique :** Utiliser _cron_ pour exécuter le script à intervalle régulier (par exemple, quotidiennement).
- **Procédure de récupération :** Fournir une méthode simple pour restaurer les données à partir d’une sauvegarde.

---

## 2. Exemple de Script de Sauvegarde (backup.sh)

Créez un fichier nommé `backup.sh` et ajoutez-y le code suivant :

```bash
#!/bin/bash
# Script de sauvegarde automatisé

# Définir le dossier source à sauvegarder et le dossier de destination
SOURCE_DIR="/chemin/vers/votre/dossier_source"
BACKUP_DIR="/chemin/vers/votre/dossier_backup"

# Créer le dossier de sauvegarde s'il n'existe pas
mkdir -p "$BACKUP_DIR"

# Définir la date du jour pour le nom du fichier
DATE=$(date +'%Y-%m-%d')
BACKUP_FILE="$BACKUP_DIR/sauvegarde_$DATE.tar.gz"

# Compresser le dossier source dans un fichier .tar.gz
tar -czf "$BACKUP_FILE" "$SOURCE_DIR"

# Afficher un message de confirmation
echo "Sauvegarde réalisée avec succès : $BACKUP_FILE"
```

**Explications :**

- `SOURCE_DIR` : Indiquez ici le chemin du dossier que vous souhaitez sauvegarder.
- `BACKUP_DIR` : Indiquez le chemin du dossier où vous voulez stocker vos sauvegardes.
- Le script crée d’abord le dossier de sauvegarde s’il n’existe pas, puis crée une archive compressée avec la date du jour dans le nom du fichier.

---

## 3. Planifier la Sauvegarde avec Cron

Pour exécuter ce script automatiquement tous les jours, éditez votre crontab en tapant :

```bash
crontab -e
```

Ajoutez ensuite la ligne suivante pour exécuter le script chaque jour à 2h du matin :

```cron
0 2 * * * /bin/bash /chemin/vers/backup.sh >> /chemin/vers/backup.log 2>&1
```

**Explications :**

- `0 2 * * *` : La tâche sera exécutée tous les jours à 02:00.
- `/bin/bash /chemin/vers/backup.sh` : Exécute le script de sauvegarde.
- `>> /chemin/vers/backup.log 2>&1` : Redirige la sortie du script vers un fichier log pour pouvoir vérifier que tout s'est bien passé.

---

## 4. Procédure de Récupération

Pour restaurer vos données à partir d'une sauvegarde, utilisez la commande suivante dans le terminal :

```bash
tar -xzf /chemin/vers/votre/dossier_backup/sauvegarde_YYYY-MM-DD.tar.gz -C /chemin/vers/dossier_destination
```

**Exemple :**

Si vous souhaitez restaurer la sauvegarde du 2025-02-10 dans le dossier `/chemin/vers/restore`, tapez :

```bash
tar -xzf /chemin/vers/votre/dossier_backup/sauvegarde_2025-02-10.tar.gz -C /chemin/vers/restore
```

