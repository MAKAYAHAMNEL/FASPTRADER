import os
import zipfile

# Définition du chemin du dossier de travail
base_dir = "/mnt/data/FTP-Site"
os.makedirs(base_dir, exist_ok=True)

# Création des fichiers HTML
html_files = {
    "index.html": """<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FTP - Accueil</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header>
        <img src="images/logo.png" alt="FTP Logo">
        <h1>Bienvenue sur FASP Trader Partners</h1>
    </header>
    <nav>
        <ul>
            <li><a href="index.html">Accueil</a></li>
            <li><a href="blog.html">Blog</a></li>
            <li><a href="about.html">À propos</a></li>
            <li><a href="contact.html">Contact</a></li>
        </ul>
    </nav>
    <main>
        <p>Il est mieux de bâtir sur du roc que sur du sable.</p>
    </main>
</body>
</html>""",
    
    "blog.html": """<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FTP - Blog</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header>
        <h1>Blog</h1>
    </header>
    <nav>
        <ul>
            <li><a href="index.html">Accueil</a></li>
            <li><a href="blog.html">Blog</a></li>
            <li><a href="about.html">À propos</a></li>
            <li><a href="contact.html">Contact</a></li>
        </ul>
    </nav>
    <main>
        <p>Articles à venir...</p>
    </main>
</body>
</html>""",
    
    "about.html": """<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FTP - À propos</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header>
        <h1>À propos de FTP</h1>
    </header>
    <nav>
        <ul>
            <li><a href="index.html">Accueil</a></li>
            <li><a href="blog.html">Blog</a></li>
            <li><a href="about.html">À propos</a></li>
            <li><a href="contact.html">Contact</a></li>
        </ul>
    </nav>
    <main>
        <p>FTP est une plateforme dédiée au trading et à la finance.</p>
    </main>
</body>
</html>""",
    
    "contact.html": """<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FTP - Contact</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header>
        <h1>Contactez-nous</h1>
    </header>
    <nav>
        <ul>
            <li><a href="index.html">Accueil</a></li>
            <li><a href="blog.html">Blog</a></li>
            <li><a href="about.html">À propos</a></li>
            <li><a href="contact.html">Contact</a></li>
        </ul>
    </nav>
    <main>
        <form>
            <label for="name">Nom :</label>
            <input type="text" id="name" name="name">
            <label for="email">Email :</label>
            <input type="email" id="email" name="email">
            <label for="message">Message :</label>
            <textarea id="message" name="message"></textarea>
            <button type="submit">Envoyer</button>
        </form>
    </main>
</body>
</html>"""
}

# Création des fichiers HTML
for filename, content in html_files.items():
    with open(os.path.join(base_dir, filename), "w", encoding="utf-8") as file:
        file.write(content)

# Création du dossier CSS et du fichier de style
css_dir = os.path.join(base_dir, "css")
os.makedirs(css_dir, exist_ok=True)

css_content = """body {
    font-family: Arial, sans-serif;
    text-align: center;
    background: #FFD700;
    color: #000;
}
header img {
    max-width: 150px;
}
nav ul {
    list-style-type: none;
    padding: 0;
}
nav ul li {
    display: inline;
    margin: 0 15px;
}
nav ul li a {
    text-decoration: none;
    font-weight: bold;
    color: black;
}"""

with open(os.path.join(css_dir, "style.css"), "w", encoding="utf-8") as file:
    file.write(css_content)

# Création du dossier JS et du fichier script.js
js_dir = os.path.join(base_dir, "js")
os.makedirs(js_dir, exist_ok=True)

js_content = """console.log('Bienvenue sur FTP!');"""

with open(os.path.join(js_dir, "script.js"), "w", encoding="utf-8") as file:
    file.write(js_content)

# Création du dossier images
images_dir = os.path.join(base_dir, "images")
os.makedirs(images_dir, exist_ok=True)

# Déplacement du fichier logo dans le dossier images
logo_path = "/mnt/data/Capture_d_écran__301_-removebg-preview.png"
new_logo_path = os.path.join(images_dir, "logo.png")
if os.path.exists(logo_path):
    os.rename(logo_path, new_logo_path)

# Création du fichier ZIP
zip_path = "/mnt/data/FTP-Site.zip"
with zipfile.ZipFile(zip_path, 'w', zipfile.ZIP_DEFLATED) as zipf:
    for root, _, files in os.walk(base_dir):
        for file in files:
            file_path = os.path.join(root, file)
            zipf.write(file_path, os.path.relpath(file_path, base_dir))

zip_path

