// CHANGE THESE TWO LINES:
const username = "whatwhatwhatwhatthef"; 
const repo = "Tools"; // Or whatever your repository is named

async function fetchTools() {
    // Corrected URL structure:
    const url = `https://api.github.com/repos/${username}/${repo}/contents/`;
    const listElement = document.getElementById('tool-list');

    try {
        const response = await fetch(url);
        
        // Safety check: If the repo isn't found or private
        if (!response.ok) {
            throw new Error(`GitHub API returned ${response.status}`);
        }

        const files = await response.json();
        listElement.innerHTML = ""; 

        files.forEach(file => {
            if (file.name.endsWith('.html') && file.name !== 'index.html') {
                const link = document.createElement('a');
                link.href = file.name;
                link.className = 'tool-card';
                
                const cleanName = file.name.replace('.html', '').replace(/%20/g, ' ');
                link.innerText = "🛠️ " + cleanName.toUpperCase();
                
                listElement.appendChild(link);
            }
        });
    } catch (error) {
        listElement.innerText = "Error: Make sure the repo 'Tools' is PUBLIC.";
        console.error(error);
    }
}
