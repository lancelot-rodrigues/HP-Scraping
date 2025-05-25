
# Scraper de Produtos HP do Mercado Livre

Este script Python foi desenvolvido para automatizar a coleta de dados de anúncios de produtos HP (especialmente cartuchos e toners, mas configurável para outros termos) em páginas do Mercado Livre. Ele navega pelas páginas de busca, coleta links de produtos e, em seguida, extrai informações detalhadas de cada página de produto, como título, preço, vendedor, avaliações e descrição. Os dados coletados são salvos em um arquivo CSV.

Este projeto faz parte do **Challenge Sprint – HP** e visa fornecer uma base de dados para análises posteriores relacionadas à identificação de possíveis casos de pirataria.

## Funcionalidades

- Busca produtos no Mercado Livre com base em uma lista de termos de pesquisa.
- Coleta links de produtos das páginas de resultados.
- Para cada produto, extrai:
  - Link do anúncio
  - Título do anúncio
  - Preço (convertido para número float)
  - Nome do vendedor
  - Nota média de avaliação e número de avaliações (quando disponíveis)
  - Descrição completa do produto (tenta clicar em "Ver descrição completa" se disponível)
- Implementa técnicas de camuflagem para reduzir a chance de detecção.
- Salva os dados coletados em um arquivo CSV formatado.

## Requisitos

- Python 3.7 ou superior
- PIP (gerenciador de pacotes Python)
- Navegador Google Chrome instalado

## Instalação de Pacotes

Antes de executar o script, instale as bibliotecas necessárias com o seguinte comando:

```bash
pip install pandas selenium webdriver-manager
```

- `pandas`: Manipulação de dados e criação do CSV.
- `selenium`: Automação de navegadores web.
- `webdriver-manager`: Gerenciamento automático do ChromeDriver.

## Configuração

### WebDriver (ChromeDriver)

O script utiliza `webdriver-manager` para baixar e configurar automaticamente o ChromeDriver compatível com sua versão do Chrome.

### Termos de Busca

A lista de termos está no bloco `if __name__ == '__main__':`, na variável `search_queries_list`. Exemplo:

```python
search_queries_list = [
    "Cartucho HP original", "Toner HP original", "Cartucho HP compativel",
    "Toner HP compativel", "Cartucho HP 664", "Cartucho HP 662",
    "Toner HP 85a", "Cartucho tinta HP"
]
```

### Modo Headless (Opcional)

O script roda em modo headless por padrão. Para visualizar o navegador, comente a linha `options.add_argument('--headless')` na função `setup_driver()`.

## Como Executar o Scraper

1. Salve o código Python (ex: `mercado_livre_scraper.py`).
2. No terminal, navegue até o diretório do arquivo.
3. Execute:

```bash
python mercado_livre_scraper.py
```

Informe quantos produtos deseja raspar por termo (pressione Enter para padrão: 2).

## Saída

Um arquivo CSV será gerado com o nome: `ml_produtos_hp_coletados_AAAAmmdd_HHMMSS.csv`.

### Colunas do CSV

- `link_anuncio`
- `titulo`
- `preco`
- `vendedor`
- `avaliacao_nota`
- `avaliacao_numero`
- `descricao`

## Importância da Camuflagem e Riscos

### Por que Camuflar?

Sites como o Mercado Livre combatem scrapers para proteger dados, evitar sobrecarga e manter a integridade da plataforma.

### Técnicas Usadas

- User-Agent comum
- Configurações do Selenium para parecer um usuário real
- Atrasos aleatórios entre ações
- Sessões isoladas de navegador

### Riscos de Detecção

- CAPTCHAs (não tratados no script)
- Bloqueio de IP
- Mudanças no HTML
- Questões legais e éticas

**Atenção:** Use o script com responsabilidade e dentro dos Termos de Serviço do site.

## Recomendações

- Não sobrecarregue o site com requisições.
- Atualize o script caso o HTML mude.
- Respeite as políticas do site.
