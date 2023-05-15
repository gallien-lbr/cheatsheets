## Useful commands linux  

### Importer un dump sur Kubernetes
`kubectl cp ~/dev/tmp_test/dump.sql.gz projet-demo/mysql-[XXXX]:/tmp/`
`zcat dump.sql.gz | mysql -uroot -proot -D BASE_DE_DONNEES`

### Vérifier ports occupés 

```
netstat -tlpn
```

### Se connecter à un serveur MySQL 
```
mysql --user=foo --password=bar --database=the_bdd_name --host=w.x.y.z
```

###  Retourner info sur mémoire vive
```
free -h
```

### Version évolué de Top en plus user friendly 
```
htop
```
### Afficher les bibliothèques utilisées par une appli
```
ldd
```
### Voir les Input / Output en écriture disque 
```
iotop  (peut nécessiter un sudo -i)
```

### Découvrir les machines du LAN 
```
nmap -sP 192.168.0.0/24
```

### Checker qui gère un nom de domaine
```
whois
```

### Compter le nombre de ligne de codes ds un rep
``` 
find . -name '*.php' | xargs wc -l
```

####  Remplacer de manière récursive une chaine de car par une autre
```
find . -type f -print0 | xargs -0 sed -i 's/titi/tutu/g'
```


### Avoir la taille des dossiers 
```
du -h --max-depth=1
```


