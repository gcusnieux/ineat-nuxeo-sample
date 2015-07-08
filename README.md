# Ineat Nuxeo Sample

Ce projet montre un exemple de packaging d'un addon Nuxeo

### Etape 1 : Générer le projet avec Nuxeo IDE

Voir la doc : https://doc.nuxeo.com/display/NXDOC/Getting+Started+with+Nuxeo+IDE

### Etape 2 : Générer le projet de packaging avec Nuxeo IDE

Voir la doc : https://doc.nuxeo.com/display/IDEDOC/Creating+a+Custom+Marketplace+Package

### Etape 3 : Créer le script de déploiement sur le canal privé

Il est désormais possible d'envoyer le package dans le canal privé.

```bash
chmod +x ineat-nuxeo-marketplace/marketplace/src/main/scripts/toMarketplace

./ineat-nuxeo-marketplace/marketplace/src/main/scripts/toMarketplace upload

HTTP/1.1 100 Continue

HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Date: Wed, 08 Jul 2015 20:12:43 GMT
Server: Apache-Coyote/1.1
Set-Cookie: JSESSIONID=8956658930F2236771771F670FC402BB.test1; Path=/nuxeo/; HttpOnly
Vary: Accept-Encoding
X-UA-Compatible: IE=10; IE=11
Content-Length: 0
Connection: keep-alive
```

Par contre la suppression ne fonctionne pas...

```bash
./ineat-nuxeo-marketplace/marketplace/src/main/scripts/toMarketplace delete
HTTP/1.1 404 Not Found
Content-Type: text/html;charset=UTF-8
Date: Wed, 08 Jul 2015 20:12:47 GMT
Server: Apache-Coyote/1.1
Set-Cookie: JSESSIONID=420DB04E17A03A172DFC0F6A3B7842EF.test1; Path=/nuxeo/; HttpOnly
Vary: Accept-Encoding
X-UA-Compatible: IE=10; IE=11
Content-Length: 2456
Connection: keep-alive
```

### Etape 4 : Corriger le script de déploiement

Pour des raisons inexpliquées notre addon et notre packaging (en version 1.0-SNAPSHOT) a la version 1.0.0-SNAPSHOT sur le canal privé

```bash
./ineat-nuxeo-marketplace/marketplace/src/main/scripts/toMarketplace delete
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Date: Wed, 08 Jul 2015 20:09:28 GMT
Server: Apache-Coyote/1.1
Set-Cookie: JSESSIONID=FCE4AD1F528B6EDC12B5543129622818.test1; Path=/nuxeo/; HttpOnly
Vary: Accept-Encoding
X-UA-Compatible: IE=10; IE=11
Content-Length: 0
Connection: keep-alive
```

Le script fonctionne...

### Etape 5 : Faire une release avec maven

On utilise un pom parent qui compile l'ensemble des modules : l'addon et le packaging

```bash
mvn release:clean release:prepare
```