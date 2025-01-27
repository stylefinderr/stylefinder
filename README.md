# stylefinder
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>StyleFinder - Din digitala stilguide</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #e74c3c;
            --accent-color: #3498db;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            background-color: #f8f9fa;
            line-height: 1.6;
        }

        /* Header */
        .header {
            background: white;
            padding: 1rem;
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
        }

        .nav-container {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            align-items: center;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--primary-color);
            text-decoration: none;
        }

        .search-filter-container {
            flex: 1;
            display: flex;
            gap: 1rem;
            max-width: 800px;
        }

        .search-bar {
            flex: 1;
            padding: 0.8rem 1.2rem;
            border: 2px solid #ddd;
            border-radius: 30px;
            font-size: 1rem;
            transition: all 0.3s;
        }

        .search-bar:focus {
            border-color: var(--accent-color);
            outline: none;
        }

        /* Filter Section */
        .filters {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
            padding: 1rem;
            max-width: 1400px;
            margin: 0 auto;
        }

        .filter-btn {
            padding: 0.5rem 1rem;
            border: 1px solid #ddd;
            border-radius: 20px;
            background: white;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .filter-btn.active {
            background: var(--primary-color);
            color: white;
            border-color: var(--primary-color);
        }

        .color-filter {
            width: 20px;
            height: 20px;
            border-radius: 50%;
            border: 2px solid #ddd;
        }

        /* Image Grid */
        .image-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 2rem;
            padding: 2rem;
            max-width: 1600px;
            margin: 0 auto;
        }

        .image-card {
            position: relative;
            border-radius: 15px;
            overflow: hidden;
            background: white;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s, box-shadow 0.3s;
        }

        .image-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 15px rgba(0, 0, 0, 0.2);
        }

        .image-card img {
            width: 100%;
            height: 400px;
            object-fit: cover;
            cursor: zoom-in;
        }

        /* Image Overlay */
        .image-overlay {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(180deg, rgba(0,0,0,0) 60%, rgba(0,0,0,0.7) 100%);
            padding: 1.5rem;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            opacity: 0;
            transition: opacity 0.3s;
        }

        .image-card:hover .image-overlay {
            opacity: 1;
        }

        .item-links {
            background: rgba(255, 255, 255, 0.9);
            padding: 1rem;
            border-radius: 10px;
            margin-top: auto;
        }

        .item-link {
            display: block;
            color: var(--primary-color);
            text-decoration: none;
            padding: 0.5rem;
            margin: 0.3rem 0;
            border-radius: 5px;
            transition: background 0.2s;
        }

        .item-link:hover {
            background: rgba(0, 0, 0, 0.05);
        }

        .tags {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
        }

        .tag {
            background: rgba(255, 255, 255, 0.9);
            padding: 0.3rem 0.7rem;
            border-radius: 15px;
            font-size: 0.9rem;
            cursor: pointer;
        }

        /* Favoriter */
        .favorite-btn {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background: none;
            border: none;
            font-size: 1.5rem;
            color: white;
            cursor: pointer;
            transition: transform 0.2s;
        }

        .favorite-btn.favorited {
            color: var(--secondary-color);
            animation: pulse 0.5s;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); }
            100% { transform: scale(1); }
        }

        /* Responsiv design */
        @media (max-width: 768px) {
            .image-grid {
                grid-template-columns: 1fr;
                padding: 1rem;
            }

            .nav-container {
                flex-direction: column;
            }

            .search-bar {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <header class="header">
        <div class="nav-container">
            <a href="#" class="logo">StyleFinder</a>
            <div class="search-filter-container">
                <input type="text" class="search-bar" placeholder="Sök efter plagg, stilar eller färger...">
                <button class="filter-btn" id="filter-btn"><i class="fas fa-sliders-h"></i></button>
            </div>
        </div>
        
        <div class="filters" id="filters">
            <button class="filter-btn" data-filter="category" value="all">Alla</button>
            <button class="filter-btn" data-filter="season" value="sommar">Sommar</button>
            <button class="filter-btn" data-filter="season" value="vinter">Vinter</button>
            <button class="filter-btn" data-filter="category" value="casual">Casual</button>
            <button class="filter-btn" data-filter="color" value="#ff0000">
                <div class="color-filter" style="background: #ff0000"></div>
            </button>
            <button class="filter-btn" data-filter="color" value="#00ff00">
                <div class="color-filter" style="background: #00ff00"></div>
            </button>
            <button class="filter-btn" data-filter="price" value="0-500">Pris 0-500 kr</button>
        </div>
    </header>

    <main>
        <div class="image-grid" id="image-grid">
            <!-- Dynamiskt inladdat innehåll -->
        </div>
        <div id="loading" style="text-align: center; padding: 2rem; display: none;">
            <i class="fas fa-spinner fa-spin"></i>
        </div>
    </main>

    <script>
        // Mockadata för demonstration
        const outfits = [
            {
                image: "https://source.unsplash.com/random/600x800?fashion",
                category: "casual",
                season: ["sommar", "vår"],
                color: "#ff0000",
                price: 299,
                links: [
                    { name: "Röd tröja - Zara", url: "#" },
                    { name: "Jeans - Levi's", url: "#" },
                    { name: "Skor - Nike", url: "#" }
                ],
                tags: ["Casual", "Röd", "Jeans"]
            },
            // Lägg till fler outfits här
        ];

        // Initiera appen
        let currentFilters = {
            category: 'all',
            season: [],
            color: [],
            price: [],
            search: ''
        };

        const grid = document.getElementById('image-grid');
        const loading = document.getElementById('loading');

        // Render outfits
        function renderOutfits(outfits) {
            grid.innerHTML = outfits.map(outfit => `
                <div class="image-card" data-category="${outfit.category}" 
                     data-season="${outfit.season.join(',')}" 
                     data-color="${outfit.color}" 
                     data-price="${outfit.price}">
                    <img src="${outfit.image}" alt="Outfit">
                    <button class="favorite-btn"><i class="far fa-heart"></i></button>
                    <div class="image-overlay">
                        <div class="tags">
                            ${outfit.tags.map(tag => `<span class="tag">${tag}</span>`).join('')}
                        </div>
                        <div class="item-links">
                            ${outfit.links.map(link => `
                                <a href="${link.url}" class="item-link" target="_blank">${link.name}</a>
                            `).join('')}
                        </div>
                    </div>
                </div>
            `).join('');
        }

        // Filtreringslogik
        function filterOutfits() {
            loading.style.display = 'block';
            setTimeout(() => {
                const filtered = outfits.filter(outfit => {
                    const matchesSearch = JSON.stringify(outfit).toLowerCase()
                        .includes(currentFilters.search.toLowerCase());
                    const matchesCategory = currentFilters.category === 'all' || 
                        outfit.category === currentFilters.category;
                    return matchesSearch && matchesCategory;
                });
                renderOutfits(filtered);
                loading.style.display = 'none';
            }, 500);
        }

        // Event listeners
        document.querySelector('.search-bar').addEventListener('input', (e) => {
            currentFilters.search = e.target.value;
            filterOutfits();
        });

        document.querySelectorAll('.filter-btn').forEach(btn => {
            btn.addEventListener('click', () => {
                btn.classList.toggle('active');
                const filterType = btn.dataset.filter;
                const value = btn.value;
                
                if (filterType === 'category' && value === 'all') {
                    currentFilters[filterType] = 'all';
                } else {
                    // Hantera flervalsfilter
                }
                
                filterOutfits();
            });
        });

        // Favoritfunktion
        document.addEventListener('click', (e) => {
            if (e.target.closest('.favorite-btn')) {
                const btn = e.target.closest('.favorite-btn');
                btn.classList.toggle('favorited');
                btn.querySelector('i').classList.toggle('far');
                btn.querySelector('i').classList.toggle('fas');
                // Spara i localStorage
            }
        });

        // Initiera första renderingen
        renderOutfits(outfits);

        // Simulera oändlig scroll
        window.addEventListener('scroll', () => {
            if (window.innerHeight + window.scrollY >= document.body.offsetHeight - 500) {
                // Ladda fler objekt
            }
        });
    </script>
</body>
</html>