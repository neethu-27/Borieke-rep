# Borieke-rep
<!DOCTYPE html>
<html lang="en" class="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Boericke Repertory App</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-white dark:bg-gray-900 text-gray-900 dark:text-gray-100 min-h-screen transition">

  <div class="max-w-3xl mx-auto p-4">
    <div class="flex justify-between items-center mb-6">
      <h1 class="text-2xl font-bold">Boericke Homeopathy Repertory</h1>
      <button onclick="toggleDarkMode()" class="bg-gray-200 dark:bg-gray-700 px-3 py-1 rounded">
        🌙 Toggle Dark Mode
      </button>
    </div>

    <input id="searchInput" type="text" placeholder="Enter symptom or remedy..." 
           class="w-full px-4 py-2 mb-4 border border-gray-300 dark:border-gray-700 rounded" 
           oninput="filterRemedies()" />

    <div id="remedyList" class="space-y-4">
      <!-- Remedies appear here -->
    </div>
  </div>

  <script>
    const remedies = [
      {
        name: "Nux Vomica",
        indications: "Irritable, oversensitive, indigestion, constipation, worse in morning",
        modalities: "Worse: after eating, anger. Better: rest, warmth"
      },
      {
        name: "Pulsatilla",
        indications: "Weepy, mild, changeable symptoms, better in open air",
        modalities: "Worse: warmth, evening. Better: fresh air, consolation"
      },
      {
        name: "Arsenicum Album",
        indications: "Anxious, restless, fear of death, food poisoning",
        modalities: "Worse: midnight, cold drinks. Better: warmth"
      }
    ];

    function displayRemedies(filtered) {
      const list = document.getElementById("remedyList");
      list.innerHTML = "";
      if (filtered.length === 0) {
        list.innerHTML = "<p>No remedies found.</p>";
        return;
      }

      filtered.forEach(remedy => {
        const card = document.createElement("div");
        card.className = "p-4 bg-white dark:bg-gray-800 rounded shadow";
        card.innerHTML = `
          <h2 class="text-xl font-semibold">${remedy.name}</h2>
          <p><strong>Indications:</strong> ${remedy.indications}</p>
          <p><strong>Modalities:</strong> ${remedy.modalities}</p>
        `;
        list.appendChild(card);
      });
    }

    function filterRemedies() {
      const input = document.getElementById("searchInput").value.toLowerCase();
      const filtered = remedies.filter(remedy =>
        remedy.name.toLowerCase().includes(input) ||
        remedy.indications.toLowerCase().includes(input) ||
        remedy.modalities.toLowerCase().includes(input)
      );
      displayRemedies(filtered);
    }

    function toggleDarkMode() {
      document.documentElement.classList.toggle('dark');
    }

    // Initial display
    displayRemedies(remedies);
  </script>

</body>
</html>