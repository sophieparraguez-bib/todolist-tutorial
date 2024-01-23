# [FR] Tutoriel "Todo list" pour débutants 😎

## 📝 Table des matières

- [Environnement](#1-environnement)
- [HTML](#2-html)
- [CSS](#3-css)
- [Javascript](#4-javascript-js)
- [Test](#5-test)

### **1. Environnement**

Pour faire ce tutoriel, nul besoin d'installer quoique ce soit sur votre machine. Le projet est déjà initialisé et prêt à l'emploi. Il vous suffit de cliquer sur le lien suivant 👉 [Todo list](https://codepen.io/sophieparraguez-bib/pen/JjzyJwz) et de suivre les instructions ci-dessous.

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
C'est parce que nous n'avons pas encore écrit la fonction en JavaScript. Pas d'inquiétudes, nous le ferons dans une prochaine étape 😎

### **3. CSS**

Ne serait-il pas plus agréable d'avoir une liste de tâches avec un peu de style ? Ajoutons donc le code CSS suivant :

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
    // Ajouter la classe "container" 👇
    <div class="container">
    // 👆 Ajouter la classe "container" 
        <h1>Liste de tâches</h1>
        <ul id="taskList"></ul>
        <input type="text" id="newTask" placeholder="Ajouter une nouvelle tâche">
        <button>Ajouter une tâche</button>
    </div>    
</body>
```

### **4. JavaScript (JS)**

Maintenant que nous avons une liste de tâches avec un peu de style, il est temps d'ajouter l'interaction. Ajoutons donc le code JavaScript suivant :

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
        // Ajouter l'attribut `onclick="addTask()"` 👇    
        <button onclick="addTask()">Ajouter une tâche</button>
        // 👆 l'attribut `onclick="addTask()"`

    </div>    
</body>
```

L'attribut `onclick` appelle la fonction `addTask` lorsque le bouton est cliqué, ce qui permet de faire fonctionner l'interaction pour l'utilisateur.

### **5. Test**

Pour vérifier que tout fonctionne correctement, vous pouvez :

- Essayez de taper une tâche dans le champ de saisie et cliquez sur "Ajouter une tâche" pour la voir ajoutée à la liste.
- Essayez de cliquer sur "Ajouter une tâche" sans rien taper dans le champ de saisie pour voir que rien ne se passe.
- Essayez de taper une tâche dans le champ de saisie et appuyez sur la touche "Entrée" pour voir que la tâche est ajoutée à la liste.