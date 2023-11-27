Question 1
La configuration par défaut d'Apache Log4j prend en charge les recherches JNDI (Java Naming and Directory Interface) qui peuvent être exploitées pour exfiltrer des données ou exécuter du code arbitraire via des services distants tels que LDAP, RMI et DNS.

**Impact:**

Un attaquant distant et non authentifié, ayant la capacité de consigner des messages spécialement conçus, peut amener Log4j à se connecter à un service contrôlé par l'attaquant pour télécharger et exécuter du code arbitraire.

**Solution:**

Dans Log4j 2.12.2 (pour Java 7) et 2.16.0 (pour Java 8 ou ultérieur), la fonctionnalité de recherche de messages a été complètement supprimée. De plus, JNDI est désactivé par défaut et d'autres paramètres de configuration par défaut sont modifiés pour atténuer CVE-2021-44228 et CVE-2021-45046.

Pour Log4j 1, supprimez la classe JMSAppender ou ne la configurez pas. Log4j 1 n'est pas pris en charge et contient probablement des bogues et des vulnérabilités non corrigés (comme CVE-2019-17571).

Pour les applications, services et systèmes utilisant Log4j, consultez le fournisseur ou le prestataire approprié. Consultez la liste des logiciels Log4j de la CISA et la section Informations sur le fournisseur ci-dessous.

**Solutions de contournement:**

Retirez la classe JndiLookup du chemin de classe, par exemple :

```bash
zip -q -d log4j-core-*.jar org/apache/logging/log4j/core/lookup/JndiLookup.class
```

À mesure que l'analyse a progressé, certaines atténuations se sont avérées moins efficaces ou incomplètes. Consultez la section "Mesures d'atténuation plus anciennes (discréditées)" sur la page des vulnérabilités de sécurité d'Apache Log4j.

SLF4J recommande également de protéger en écriture les fichiers de configuration Log4j.


Question2
 Le problème examiner  est le problème [COLLECTIONS-813] (https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-813?filter=doneissues) dans le cadre du projet Apache Commons Collections.
Cette anomalie est de portée locale, étant donné qu'elle est confinée à une zone spécifique.
L'origine de ce problème résidait dans une NullPointerException qui n'était pas déclenchée. La résolution a consisté à introduire des protections afin de garantir que, lorsqu'une valeur est nulle, une exception est levée. Les collaborateurs ont également ajouté de nouveaux tests et ajusté ceux déjà existants dans le but de repérer ce problème dans les versions futures.

Question3

Netflix mène des expériences d'ingénierie du chaos, comprenant Chaos Monkey, Chaos Kong et des tests d'injection de défaillance. Les exemples impliquent la terminaison d'instances de machines virtuelles, la simulation de pannes de régions Amazon EC2 et l'injection de latence entre les services.
Les expériences ont lieu dans l'environnement de production, nécessitant des conditions réelles. Observer les métriques en état stable, la réponse du système aux défaillances et l'expérience utilisateur sont essentiels
Netflix atteint ses objectifs d'amélioration de la résilience du système, d'assurance d'une dégradation en douceur et de renforcement de la confiance dans les capacités de production.
Amazon, Google, Microsoft et Facebook appliquent également l'ingénierie du chaos.

Question 4

L'avantage d'avoir une spécification formelle pour WebAssembly réside dans le fait que le langage, étant bien construit, peut être sécurisé, rapide, portable et compact. Ainsi, étant donné que l'architecture est éprouvée, aucun bug ne peut en découler.

Cependant, cela ne signifie pas qu'une spécification formelle ne doit pas être testée, car une implémentation peut contenir des bugs.


Question 5
La principale utilité de la spécification mécanisée réside dans sa capacité à contraindre le développeur à expliciter ses hypothèses, réduisant ainsi les erreurs. Cette approche améliore la spécification formelle d'origine, étant donné qu'elle est validée par un ordinateur, plus rapide et capable de vérifier efficacement toutes les évolutions futures. Divers outils, tels qu'un vérificateur de type exécutable et un interpréteur exécutable, bénéficient également de cette spécification mécanisée. L'auteur procède à la vérification de la spécification en exécutant ces éléments. Bien que cette nouvelle spécification réduise considérablement les erreurs d'implémentation.
