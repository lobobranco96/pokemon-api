# PokeAPI Data 

## Descrição

Este projeto busca e compila dados de Pokémon a partir da [PokeAPI](https://pokeapi.co/). O objetivo é recuperar informações sobre as gerações disponíveis, as regiões correspondentes e detalhes de cada Pokémon.

## Estrutura do Projeto

O projeto é composto por duas funções principais:

### 1. `fetch_pokemon_from_api()`

Esta função faz uma requisição à PokeAPI para obter todas as gerações de Pokémon disponíveis. Ela retorna um dicionário contendo duas listas:

- `"region"`: Nomes das regiões correspondentes a cada geração.
- `"pokemon_id"`: IDs dos Pokémon em cada geração.

### 2. `fetch_poke(region, pokemon_id)`

Esta função busca dados detalhados de um Pokémon específico a partir da PokeAPI. Ela recebe como argumentos a região e o ID do Pokémon, e retorna um dicionário com informações como:

- Nome
- Altura
- Peso
- Experiência base
- Tipos
- Habilidades
- Movimentos
- Áreas onde pode ser encontrado
- Evoluções e se é mítico ou lendário.

## Funcionalidade

- **Busca de Gerações**: A função `fetch_pokemon_from_api()` obtém uma lista de gerações e, para cada geração, busca a região e os IDs dos Pokémon.
  
- **Detalhes do Pokémon**: A função `fetch_poke(region, pokemon_id)` coleta informações detalhadas sobre cada Pokémon, incluindo suas habilidades, movimentos e áreas de encontro.

## Exemplo de Uso

Para utilizar as funções do projeto, você precisa ter as bibliotecas `requests` e `pandas` instaladas. A seguir, um exemplo de como utilizar as funções:

```python
# Chama a função para buscar dados de Pokémon
complete_dicionario = fetch_pokemon_from_api()

# Loop pelas regiões disponíveis
for region_index in range(len(complete_dicionario['region'])):
    all_pokemon_data = []
    region = complete_dicionario['region'][region_index]

    for pokemon_id in complete_dicionario['pokemon_id'][region_index]:
        pokemon_data = fetch_poke(region, pokemon_id)
        all_pokemon_data.append(pokemon_data)

    dataframe = pd.DataFrame(all_pokemon_data)
    # Salva os dados em um arquivo JSON
    dataframe.to_json(f"{region}.json", orient='records', lines=True)

