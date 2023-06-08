# Olá, eu sou o Fabricio Torres!

- Atualmente trabalho como Suporte Tecnico/QA/Desenvolvedor
- Estudante de Analise e Desnvolvimento de Sistemas (FIAP)

<?php

// Substitua o valor abaixo pelo seu nome de usuário do GitHub
$username = 'Fabs0602';

// Faz uma solicitação à API do GitHub para recuperar as informações do perfil
$profileData = file_get_contents("https://api.github.com/users/{$username}");
$profileData = json_decode($profileData, true);

// Verifica se o perfil foi encontrado
if (isset($profileData['login'])) {
    // Recupera a contagem total de commits
    $totalCommits = $profileData['total_private_repos'] + $profileData['public_repos'];

    // Recupera a lista de linguagens de programação
    $languageData = file_get_contents("https://api.github.com/users/{$username}/repos");
    $languageData = json_decode($languageData, true);

    $languageStats = array();

    // Calcula a contagem total de linhas de código para cada linguagem
    foreach ($languageData as $repo) {
        $repoLanguages = file_get_contents($repo['languages_url']);
        $repoLanguages = json_decode($repoLanguages, true);

        foreach ($repoLanguages as $language => $lines) {
            if (isset($languageStats[$language])) {
                $languageStats[$language] += $lines;
            } else {
                $languageStats[$language] = $lines;
            }
        }
    }

    // Adiciona a linguagem JavaScript aos dados estatísticos se ainda não estiver presente
    if (!isset($languageStats['JavaScript'])) {
        $languageStats['JavaScript'] = 0;
    }

    // Calcula a porcentagem de cada linguagem
    $languagePercentages = array();

    foreach ($languageStats as $language => $lines) {
        $percentage = round(($lines / array_sum($languageStats)) * 100, 2);
        $languagePercentages[$language] = $percentage;
    }

    // Exibe a porcentagem de cada linguagem
    foreach ($languagePercentages as $language => $percentage) {
        echo "{$language}: {$percentage}%<br>";
    }
} else {
    echo "Perfil não encontrado.";
}

?>

  
  ![snake svg](https://github.com/Fabs0602/Fabs0602/blob/output/github-contribution-grid-snake.svg)
