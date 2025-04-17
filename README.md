<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contagem de Medalhas - Ranking</title>
</head>
<body>
  <h1>Contagem de Medalhas</h1>

  <div>
    <label for="pais">Nome do País:</label>
    <input type="text" id="pais"><br><br>

    <label for="ouro">Medalhas de Ouro:</label>
    <input type="number" id="ouro"><br><br>

    <label for="prata">Medalhas de Prata:</label>
    <input type="number" id="prata"><br><br>

    <label for="bronze">Medalhas de Bronze:</label>
    <input type="number" id="bronze"><br><br>

    <button onclick="adicionarMedalhas()">Adicionar Medalhas</button>
    <button onclick="mostrarRanking()">Mostrar Ranking</button>
  </div>

  <h2 id="resultado"></h2>
  
  <h3 id="ranking"></h3>

  <script>
    let paises = [];

    function adicionarMedalhas() {
      const pais = document.getElementById('pais').value;
      const ouro = parseInt(document.getElementById('ouro').value) || 0;
      const prata = parseInt(document.getElementById('prata').value) || 0;
      const bronze = parseInt(document.getElementById('bronze').value) || 0;

      if (pais === "") {
        alert("Por favor, insira o nome do país.");
        return;
      }

      const totalMedalhas = ouro + prata + bronze;

      // Adiciona o país e o total de medalhas ao array
      paises.push({ nome: pais, total: totalMedalhas });

      // Limpa os campos de entrada
      document.getElementById('pais').value = '';
      document.getElementById('ouro').value = '';
      document.getElementById('prata').value = '';
      document.getElementById('bronze').value = '';

      document.getElementById('resultado').innerText = `${pais} adicionou ${totalMedalhas} medalhas.`;
    }

    function mostrarRanking() {
      if (paises.length === 0) {
        alert("Nenhum país foi adicionado.");
        return;
      }

      // Ordena os países pelo total de medalhas de forma decrescente
      paises.sort((a, b) => b.total - a.total);

      let rankingTexto = "#Ranking de Medalhas:\n";

      paises.forEach((pais) => {
        rankingTexto += `#${pais.nome}: ${pais.total} medalhas\n`;
      });

      // Exibe o ranking na tela
      document.getElementById('ranking').innerText = rankingTexto.replace(/\n/g, '<br>');
    }
  </script>
</body>
</html>
