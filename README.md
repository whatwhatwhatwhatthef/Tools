<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vibecodes Dynamic Hub</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; padding: 20px; background: #0d1117; color: #c9d1d9; text-align: center; }
        .container { max-width: 500px; margin: auto; }
        .tool-card { 
            display: block; background: #21262d; color: #58a6ff; 
            padding: 20px; margin: 10px 0; border-radius: 6px; 
            text-decoration: none; border: 1px solid #30363d; font-weight: bold;
            transition: 0.3s;
        }
        .tool-card:hover { background: #30363d; border-color: #8b949e; transform: scale(1.02); }
        .loader { color: #8b949e; font-style: italic; }
    </style>
</head>
<body>

<div class="container">
    <h1>Vibecodes Tool Hub</h1>
    <p>Automatically detecting new tools...</p>
    <div id="tool-list" class="loader">Scanning repository...</div>
</div>

<script>
    // EDIT THESE TWO LINES:
    const username = "YOUR_GITHUB_USERNAME"; 
    const repo = "YOUR_REPO_NAME";

    async function fetchTools() {
        const url = `https://api.github.com/repos/whatwhatwhatwhatthef.github.io/Tools/contents/`;
        const listElement = document.getElementById('tool-list');

        try {
            const response = await fetch(url);
            const files = await response.json();
            
            listElement.innerHTML = ""; // Clear loader

            files.forEach(file => {
                // Only show .html files, and don't list index.html itself
                if (file.name.endsWith('.html') && file.name !== 'index.html') {
                    const link = document.createElement('a');
                    link.href = file.name;
                    link.className = 'tool-card';
                    
                    // Make the name look pretty (remove .html and replace %20)
                    const cleanName = file.name.replace('.html', '').replace(/%20/g, ' ');
                    link.innerText = "🛠️ " + cleanName.toUpperCase();
                    
                    listElement.appendChild(link);
                }
            });
        } catch (error) {
            listElement.innerText = "Error loading tools. Check your username/repo name.";
            console.error(error);
        }
    }

    fetchTools();
</script>

</body>
</html>
