# TP2-exam
Bloquer les crawler avec Apache2

### 1. Aller sur les fichier log (Apache2)
```
# /var/log/apache2
```
On trouve les fichier: access.log, error.log, other_vhosts_access.log

### 2. Créer un fichier qui s’occupe du blocage
```
# nano blockCrawler.sh
```

### 3. Ajouter les configurations
```
# !/bin/sh
cat /var/log/apache2/access.log | grep ".*bot*" | sed "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\" | awk '{print $1}' | uniq | sort | tail -n 100 | iptables -A INPUT $1 -j Done;
```

### 4. Donner accès au fichier
```
# chmod +x blockCrawler.sh
```

### 5. Lancer la commande
```
# blockCrawler.sh
```