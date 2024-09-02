
# Envoy Proxy - Guide d'Installation et de Lancement

Ce guide vous expliquera comment installer et lancer Envoy Proxy avec un fichier de configuration personnalisé. 

## Prérequis

- Un environnement Linux ou macOS.
- `curl` installé pour tester les endpoints.
- Droits d'administration pour installer Envoy.

## Installation d'Envoy Proxy

### Étape 1: Installer Envoy Proxy

Pour installer Envoy Proxy, suivez les étapes ci-dessous :

### Sous macOS avec Homebrew

```bash
brew install envoy
```

### Sous Linux (exemple avec Ubuntu)

Ajoutez le dépôt officiel d'Envoy :

```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
curl -sL 'https://getenvoy.io/gpg' | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.getenvoy.io/public/deb/ubuntu $(lsb_release -cs) main"
sudo apt-get update
sudo apt-get install -y getenvoy-envoy
```

### Étape 2: Vérifier l'installation

Pour vérifier que Envoy est bien installé, lancez la commande suivante :

```bash
envoy --version
```

Vous devriez voir la version d'Envoy installée s'afficher.

## Lancer Envoy Proxy

### Étape 1: Préparer la configuration

Assurez-vous d'avoir un fichier de configuration, par exemple `envoy-weebi.yaml`, dans le répertoire courant.

### Étape 2: Lancer Envoy avec la configuration

Lancez Envoy en utilisant le fichier de configuration :

```bash
envoy -c envoy-weebi.yaml --log-path logs/custom.log
```

### Étape 3: Valider la configuration

Vous pouvez valider la configuration sans lancer Envoy en mode proxy avec la commande suivante :

```bash
envoy --mode validate -c envoy-weebi.yaml
```

### Étape 4: Tester le Proxy

Pour tester que Envoy est bien en cours d'exécution, vous pouvez utiliser `curl` pour effectuer des requêtes HTTP sur les ports configurés. Par exemple :

```bash
curl -v 0.0.0.0:9902
```

```bash
curl -v 0.0.0.0:8082
```

Ces commandes devraient retourner une réponse de Envoy si le proxy est correctement configuré et en cours d'exécution.

## Logs et Débogage

Les logs d'Envoy sont écrits dans le fichier spécifié avec l'option `--log-path`. Par exemple, `logs/custom.log` dans notre commande ci-dessus. Vous pouvez consulter ces logs pour déboguer ou surveiller l'activité d'Envoy.

```bash
tail -f logs/custom.log
```

## Ressources supplémentaires

Pour plus d'informations sur la configuration et l'utilisation d'Envoy Proxy, vous pouvez consulter la documentation officielle : [https://www.envoyproxy.io/docs](https://www.envoyproxy.io/docs)
