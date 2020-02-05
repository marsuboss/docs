---
id: version-18.0-plug-ins
title: Plug-ins
original_id: plug-ins
---

En développant une application 4D, vous découvrirez de nombreuses fonctionnalités que vous n'aviez pas remarquées au début. You can even augment the standard version of 4D by adding **plug-ins** to your 4D development environment.

## Pourquoi un plugin ?

Bien que 4D propose des centaines de méthodes intégrées permettant de manipuler des objets et des enregistrements, et d'implémenter une interface utilisateur, une utilisation ou des fonctionnalités spéciales (parfois dépendantes de la plate-forme) peuvent être nécessaires : l'une peut nécessiter ODBC sous Windows, une autre peut nécessiter des services Apple sous macOS, et un autre peut souhaiter implémenter des outils statistiques spécifiques, une connexion à un réseau social, une plateforme de paiement, un accès à un fichier sur le réseau, une interface utilisateur spéciale ou une structure d'image privée.

Il est évident que couvrir tous les domaines des systèmes d'exploitation macOS et Windows au moyen de commandes 4D mènerait certainement à un produit contenant des milliers de commandes et, dans le même temps, la plupart des utilisateurs n'auraient pas besoin d'un si grand ensemble de fonctionnalités. De plus, la création d'un outil aussi complet rendrait l'environnement 4D incroyablement complexe et demanderait des mois d'étude à la plupart des utilisateurs avant de pouvoir obtenir des résultats utiles.

La nature modulaire de l'environnement 4D permet la création d'applications de base, mais n'exclut pas le développement de systèmes extrêmement complexes. L'architecture du plug-in 4D ouvre l'environnement 4D à tout type d'application ou d'utilisateur. Les plug-ins 4D multiplient la puissance et la productivité de cette application ou de l'utilisateur.

## Qu'est-ce qu'un plug-in et à quoi sert-il ?

Un plug-in est un morceau de code que 4D lance au démarrage. Il ajoute des fonctionnalités à 4D et augmente ainsi sa capacité.

Habituellement, un plug-in fait des choses :
- Que 4D ne peut pas effectuer (c'est-à-dire une technologie de plate-forme spécifique),
- Qui sera très difficile à écrire en utilisant uniquement 4D,
- Qui sont uniquement disponibles en tant que point d'entrée de plug-in

Un plug-in contient généralement un ensemble de routines données au développeur 4D. Il peut gérer une zone externe et exécuter un processus externe.

- A **plug-in routine** is a routine written in native language (usually C or C++) that causes an action.
- An **external area** is a part of a form that can display almost everything and interact with the user when necessary.
- An **external process** is a process that runs alone, usually in a loop, doing almost everything it wants. Tout le code de process appartient au plug-in, 4D est simplement présent pour recevoir/envoyer des événements au process.

### Note importante

Un plug-in peut être très simple, avec une seule routine effectuant une très petite tâche, ou très complexe, impliquant une centaine de routines et de domaines. Les capacités d'un plug-in sont pratiquement sans limite. Cependant, chaque développeur de plug-in doit se rappeler qu'un plug-in est un "échantillon" de code. C'est le plug-in qui s'exécute dans 4D, et non l'inverse. En tant que morceau de code, c'est l'hôte de 4D; ce n'est pas une application autonome. Il partage le temps CPU et la mémoire avec 4D et d'autres plug-ins. Il doit donc s'agir d'un code poli, qui utilise exactement ce qui est nécessaire à son fonctionnement. Par exemple, dans les longues boucles, un plug-in doit appeler `PA_Yield ()` pour donner du temps au planificateur 4D, à moins que sa tâche ne soit critique aussi bien pour lui que pour la base de données.

## Comment créer un plug-in ?

4D provides on GitHub an open-source [**plug-in SDK**](https://github.com/4d/4D-Plugin-SDK), containing the 4D Plugin API and the 4D Plugin Wizard:

- the [**4D Plugin API**](https://github.com/4d/4D-Plugin-SDK/blob/master/4D%20Plugin%20API), written in C, adds more than 400 functions that help you to easily create your own plug-ins to add new functionnalities to your 4D application. Les fonctions du plug-in API de 4D gèrent toutes les interactions entre l'application 4D et votre plug-in.
- The [**4D Plugin Wizard**](https://github.com/4d/4D-Plugin-SDK/blob/master/4D%20Plugin%20Wizard) is an essential tool that simplifies the task of developing 4D plug-ins. Il écrit le code dont 4D a besoin pour interagir correctement avec un plug-in et le charger, afin de vous concentrer sur votre propre code.

## Comment installer un plug-in?

L’installation des plug-ins et composants dans l’environnement 4D s’effectue par simple copie des fichiers des plug-ins ou des composants dans des dossiers appropriés.

Les dossiers “NomPlugin.bundle” (appelés paquets ou packages sous Mac Os) contiennent à la fois les versions Windows et Mac Os des plug-ins 4D. Leur architecture interne spécifique permet notamment à 4D Server de charger la version adéquate en fonction de la plate-forme d’exécution du poste client. To install a plug-in in your environment, you just need to put the “PluginName.bundle” folder or package concerned into the desired **PlugIns** folder.

Vous pouvez placer les dossiers PlugIns et Components à deux endroits :

- Au niveau de l’application 4D exécutable, c'est-à-dire .:
  - Sous Windows : à côté du fichier .exe
  - Under macOS: at the first level of the Contents folder inside the application package. In this case, plug-ins are available in every database opened by this application.
- Au même niveau que le fichier de structure de la base. Dans ce cas, les plug-ins et les composants sont disponibles dans cette base de données uniquement.

Le choix de l’emplacement dépend de votre mode d’utilisation du plug-in ou du composant.

Si un même plug-in ou un même composant est placé aux deux endroits, 4D charge uniquement celui situé à côté de la structure. Dans le cas d’une application compilée et fusionnée avec 4D Volume Desktop, la présence de plusieurs instances d’un même plug-in ou d'un même composant empêchera l’ouverture de l’application.

Les plug-ins et les composants sont chargés par 4D lors du lancement de l’application. Vous devez donc quitter votre application 4D avant d’effectuer vos copies de fichiers ou dossiers. Ouvrez ensuite votre base de données avec 4D. Si l’utilisation d'un plug-in nécessite une licence spécifique, le plug-in est chargé mais n’est pas actif.