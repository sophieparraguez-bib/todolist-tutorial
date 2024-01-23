# [FR] Tutoriel "Todo list" pour débutants 😎

## Disclaimer

Ce tutoriel a été élaboré dans le cadre de ma participation au programme _**Numerique@Michelin - Mon stage 100% Filles**_, dont l'objectif est de sensibiliser les jeunes filles aux métiers du numérique.  
Il est donc destiné à des débutants en développement, qui souhaitent apprendre à coder. L'objectif étant de créer une liste de tâches très simple en HTML, CSS et JavaScript.  
Il est conçu pour être suivi pas à pas, en commençant par les bases et en ajoutant progressivement des fonctionnalités supplémentaires.

## 📝 Table des matières

- [Environnement](#1-environnement)
- [HTML](#2-html)
- [CSS](#3-css)
- [Javascript](#4-javascript-js)
- [Test](#5-test)
- [Bonus 1](#6-bonus-1)
- [Bonus 2](#7-bonus-2)

### **1. Environnement**

Pour faire ce tutoriel, nul besoin d'installer quoique ce soit sur votre machine.  
Le projet est déjà initialisé et prêt à l'emploi. Il vous suffit d'ouvrir le lien suivant 👉 [Environnement live CodePen](https://codepen.io/sophieparraguez-bib/pen/JjzyJwz) et de suivre les instructions ci-dessous.

> Pour ceux qui souhaitent en savoir plus, [CodePen](https://codepen.io/) est une plateforme en ligne qui permet de coder en mode bac à sable directement sur votre navigateur.

Une fois le lien CodePen ouvert, vous verrez 3 fenêtres :

- `HTML` : C'est le fichier HTML principal qui structure le contenu de votre page web.

- `CSS` : C'est le fichier CSS qui ajoute des styles pour rendre votre liste de tâches agréable à l'œil.

- `JS` : C'est le fichier JavaScript qui ajoute l'interaction à votre liste de tâches.

En dessous de ces 3 fenêtres, vous verrez l'aperçu de votre liste de tâches mais pour l'instant il n'y a rien à voir 😎

### **2. HTML**

Commençons par remplir le fichier HTML avec le code suivant :

```html
<body>
    <div>
        <h1>Liste de tâches</h1>
        <ul id="taskList"></ul>
        <input type="text" id="newTask" placeholder="Ajouter une nouvelle tâche">
        <button>Ajouter une tâche</button>
    </div>    
</body>
```

Explications des balises :

- **`<body>` :** Contient le contenu visible de votre page web.
- **`<div class="container">` :** Un conteneur pour regrouper et styliser le contenu.
- **`<h1>Liste de tâches</h1>` :** L'en-tête principal de votre page web.
- **`<ul id="taskList"></ul>` :** Une liste non ordonnée vide où les tâches seront ajoutées.
- **`<input type="text" id="newTask" placeholder="Ajouter une nouvelle tâche">` :** Un champ de saisie de texte pour que les utilisateurs puissent taper de nouvelles tâches.
- **`<button>Ajouter une tâche</button>` :** Un bouton qui sera utilisé pour ajouter une tâche lorsqu'il est cliqué.

Comme vous pouvez le voir dans l'aperçu, nous avons maintenant, un titre, un champ de saisie de texte ainsi qu'un bouton.
Mais lorsque vous cliquez sur le bouton, rien ne se passe 😓  
C'est parce que nous n'avons pas encore écrit la fonction en JavaScript. Pas d'inquiétude, nous le ferons dans une prochaine étape 😎

### **3. CSS**

Ne serait-il pas plus agréable d'avoir une liste de tâches avec un peu de style ?  

Ajoutons donc le code CSS suivant :

```css
body {
    font-family: 'Arial', sans-serif;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
    background-color: #f4f4f4;
}

.container {
    text-align: center;
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
    color: #333;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    background-color: #e6e6e6;
    margin: 8px 0;
    padding: 8px;
    border-radius: 4px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

input[type="text"] {
    padding: 8px;
    margin-right: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    padding: 8px 16px;
    background-color: #4caf50;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}
```

Explications des sélecteurs CSS :

- **`body` :** Définit la police, centre le contenu et fournit une couleur de fond légère.
- **`.container` :** Centre le contenu, lui donne un fond blanc, un remplissage, des coins arrondis et une légère ombre.
- **`h1` :** Définit la couleur de l'en-tête principal.
- **`ul` :** Supprime le style de liste par défaut et la marge.
- **`li` :** Stylise chaque élément de tâche avec une couleur de fond légère, une marge, un remplissage, des coins arrondis et un affichage flex pour un meilleur alignement.
- **`input[type="text"]` :** Stylise le champ de saisie de texte avec un remplissage, une marge, une bordure et un bord arrondi.
- **`button` :** Stylise le bouton avec un remplissage, une couleur de fond, une couleur de texte, une bordure, un bord arrondi et un curseur en pointeur.

Comme nous avons ajouter une classe css `container`, nous devons modifier le fichier HTML pour ajouter cette classe à notre div :

```html
<body>
    <!-- Ajouter 'class="container"' 👇 -->
    <div class="container">
    <!-- 👆 Ajouter 'class="container"' -->
        <h1>Liste de tâches</h1>
        <ul id="taskList"></ul>
        <input type="text" id="newTask" placeholder="Ajouter une nouvelle tâche">
        <button>Ajouter une tâche</button>
    </div>    
</body>
```

### **4. JavaScript (JS)**

Maintenant que nous avons une liste de tâches avec un peu de style, il est temps d'ajouter l'interactivité. 

Ajoutons donc le code JavaScript suivant :

```javascript
function addTask() {

    const newTaskInput = document.getElementById("newTask");
    const taskList = document.getElementById("taskList");
    
    if (newTaskInput.value !== "") {

        const taskItem = document.createElement("li");

        taskItem.textContent = newTaskInput.value;
        taskList.appendChild(taskItem);
        newTaskInput.value = "";
    }
}
```

Explications du code JavaScript :

- **`function addTask()` :** Définit une fonction JavaScript nommée `addTask`.
- **`const newTaskInput = document.getElementById("newTask");` :** Récupère l'élément d'entrée avec l'identifiant "newTask" et le stocke dans la variable `newTaskInput`.
- **`const taskList = document.getElementById("taskList");` :** Récupère la liste non ordonnée avec l'identifiant "taskList" et la stocke dans la variable `taskList`.
- **`if (newTaskInput.value !== "") { ... }` :** Vérifie si le champ de saisie n'est pas vide.
- **`const taskItem = document.createElement("li");` :** Crée un nouvel élément de liste.
- **`taskItem.textContent = newTaskInput.value;` :** Définit le contenu texte du nouvel élément de liste sur la valeur du champ de saisie.
- **`taskList.appendChild(taskItem);` :** Ajoute le nouvel élément de liste à la liste des tâches.
- **`newTaskInput.value = "";` :** Réinitialise le champ de saisie après avoir ajouté une tâche.

Maintenant que nous avons écrit le code JavaScript, nous devons le lier à notre fichier HTML. Pour ce faire, nous allons ajouter un attribut `onclick` à notre bouton :

```html
<body>
    <div class="container">
        <h1>Liste de tâches</h1>
        <ul id="taskList"></ul>
        <input type="text" id="newTask" placeholder="Ajouter une nouvelle tâche">
        <!-- Ajouter 'onclick="addTask()"' 👇 -->  
        <button onclick="addTask()">Ajouter une tâche</button>
        <!-- 👆 Ajouter 'onclick="addTask()"' -->

    </div>    
</body>
```

L'attribut `onclick` appelle la fonction `addTask` lorsque le bouton est cliqué, ce qui permet de créer l'interaction pour l'utilisateur.

### **5. Test**

Pour vérifier que tout fonctionne correctement, vous pouvez :

- Essayer de taper une tâche dans le champ de saisie et cliquez sur "Ajouter une tâche" pour la voir ajoutée à la liste.
- Essayer de cliquer sur "Ajouter une tâche" sans rien taper dans le champ de saisie pour voir que rien ne se passe.
- Essayer de taper une tâche dans le champ de saisie et appuyez sur la touche "Entrée" pour voir que la tâche est ajoutée à la liste.

Félicitations 🎉

Vous avez terminé le tutoriel "Todo list" pour débutants 😎

### **6. Bonus 1**

Maintenant que vous avez terminé le tutoriel, vous souhaiter peut être ajouter une fonctionnalité supplémentaire à votre liste de tâches ?  
Nous pouvons, par exemple, ajouter un bouton pour supprimer une tâche de la liste.

Comme il s'agit d'une interaction utilisateur, nous allons devoir modifier le code Javascript pour lui ajouter une fonction "supprimer", puis faire le lien entre la fonction et l'interface utilisateur.

Ajoutons le code JavaScript suivant à notre code existant :

```javascript
function addTask() {

    const newTaskInput = document.getElementById("newTask");
    const taskList = document.getElementById("taskList");
    
    if (newTaskInput.value !== "") {

        const taskItem = document.createElement("li");
        taskItem.textContent = newTaskInput.value;

        // Ajouter ce code 👇
        // Ajoute un bouton de suppression à chaque tâche dans le code HTML
        taskItem.innerHTML += '<button id="deleteTask" onclick="deleteTask(this)">Supprimer</button>';
        // 👆 Ajouter ce code

        taskList.appendChild(taskItem);
        newTaskInput.value = "";
    }
}

// Ajouter ce code 👇
function deleteTask(taskItem) {
   const taskList = document.getElementById("taskList");
   taskList.removeChild(taskItem.parentElement);
}
// 👆 Ajouter ce code 
```

Explications du code JavaScript :

- **`taskItem.innerHTML += '<button onclick="deleteTask(this)">Supprimer</button>';` :** Ajoute un bouton de suppression directement dans le code HTML de la tâche en utilisant la propriété `innerHTML`. Le bouton appelle la fonction `deleteTask(this)` lorsqu’il est cliqué, en se passant lui-même comme paramètre (avec le mot clé `this`).
- La fonction **`deleteTask(taskItem)`** est responsable de supprimer la tâche correspondante lorsque le bouton “Supprimer” est cliqué. Elle utilise `taskList.removeChild(taskItem.parentElement)`; pour retirer l’élément `<li>` parent de celui qui a déclenché la fonction (le bouton).

>👋 En utilisant cette approche, le bouton “Supprimer” est généré directement dans le code HTML, ce qui peut rendre le code plus lisible et maintenable, tout en se rapprochant des techniques de développement web modernes (React, Vue etc..).

### **7. Bonus 2**

Maintenant que nous avons toutes ces fonctionnalités, nous pouvons essayer d'améliorer l'expérience utilisateur en jouant avec différents styles pour rendre la liste de tâches plus attrayante.   
Pour cela nous allons modifier le code CSS que nous avons déjà écrit.

1 - Modifiez la couleur de fond de la page (body):

```css
body {
    /* ... Code existant non affiché */   
    background-color: DarkSlateBlue;
}
```

>👋 Les noms et code de couleurs HTML sont disponibles ici 👉 [HTML Noms de couleurs](https://htmlcolorcodes.com/fr/noms-de-couleur/)

2 - Donnez une taille (fixe) au conteneur de la liste de tâches :

```css
.container {
    /* ... Code existant non affiché */
    width: 600px;
}
```

3 - Changer la couleur du titre (h1) :

```css
h1 {
    color: teal;
}
```

4 - Remplacer le style des tâches et de la case de saisie de texte :

```css
li {
   background-color: lavender; /* 👈 Changement de couleur de fond */
   margin: 10px 0; /* 👈 Augmentation des marges extérieures */
   padding: 10px; /* 👈 Augmentation des marges intérieures */
   border-radius: 8px; /* 👈 Coins plus arrondis */
   box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); /* 👈 Ajout d'une ombre */
   display: flex;
   justify-content: space-between;
   align-items: center;
}
input[type="text"] {
   padding: 10px; /* 👈 Augmentation des marges intérieures */
   margin-right: 10px; /* 👈 Augmentation de la marge extérieure droite */
   border: 1px solid #ccc;
   border-radius: 8px;
}
```

5 - Remplacer le style du bouton d'ajout de tâche :

```css
button {
   padding: 10px 20px; /* 👈 Augmentation des marges intérieures */
   background-color: #008000; /* 👈 Changement de couleur de fond */
   color: #fff;
   border: none;
   border-radius: 8px; /* 👈 Coins plus arrondis */
   cursor: pointer;
   transition: background-color 0.3s ease; /* 👈 Ajout d'une transition */
}

button:hover {
   background-color: #006400; /* 👈 Changement de couleur de fond au survol */
}

```

Ici nous avons ajouté une transition sur le bouton d'ajout de tâche. Cela permet d'ajouter un effet d'animation lorsque le bouton est survolé par la souris.

6 - Ajout d'une couleur spécfique pour le bouton de suppression de tâche :

```css
button#deleteTask {
    background-color: #e74c3c;
}
button#deleteTask:hover {
    background-color: #c0392b;
}
```

Comme nous avons déjà défini un style pour tous les boutons, nous devons ajouter un sélecteur CSS spécifique pour le bouton de suppression de tâche. Nous utilisons donc l'identifiant `#deleteTask` pour cibler ce bouton en particulier.

Voilà ! Vous avez maintenant une liste de tâches avec un style plus attrayant 😍

N'hésitez pas à expérimenter davantage en continuant de jouer avec les valeurs des propriétés CSS et en observant comment elles affectent l'apparence de votre liste de tâches.
