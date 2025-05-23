# Editor Dinâmico de Layout de Ônibus

Este projeto é uma aplicação web para criar e editar visualmente layouts de assentos de ônibus de forma dinâmica. Ele permite adicionar, remover, habilitar/desabilitar assentos, posicionar portas e nomear os mapas de layout.

## Funcionalidades Principais

* **Visualização Gráfica:** Exibe o layout do ônibus com assentos em duas seções (esquerda e direita), simulando o corredor central. [cite: 97, 102]
* **Edição de Assentos:**
    * **Adicionar Assentos:** Clique em um espaço vazio para adicionar um novo assento, solicitando a numeração. [cite: 179, 180]
    * **Remover Assentos:** Remove um assento existente, transformando-o em um espaço vazio, mantendo os botões de ação (+/-). [cite: 137, 138, 139, 140, 141]
    * **Habilitar/Desabilitar Assentos:** Altera o status de um assento entre habilitado e desabilitado através de um menu de contexto. [cite: 195, 197, 198, 199, 200] Os assentos desabilitados são visualmente distintos (cor vermelha). [cite: 37]
    * **Renomear Assentos:** Permite clicar no número do assento para alterar sua numeração. [cite: 207, 208]
* **Gerenciamento de Portas:**
    * Adiciona indicadores visuais de portas (Entrada 1, Entrada 2) em posições específicas adjacentes aos assentos. [cite: 112, 113, 114, 115, 183, 162]
    * Os botões para adicionar portas aparecem apenas em assentos candidatos pré-definidos. [cite: 8, 9, 111, 112, 113, 114, 115]
* **Nome do Mapa:** Permite ao usuário definir um nome para o layout que está sendo criado/editado. [cite: 11, 85, 86, 87]
* **Menu de Contexto:** Ao clicar em um assento, um menu de contexto aparece com opções para "Habilitar/Desabilitar Assento" e "Remover Assento". [cite: 94, 173, 174]
* **Legenda:** Uma legenda detalhada explica o significado das diferentes cores e símbolos usados para assentos e portas. [cite: 121, 122, 123, 124, 125]
* **Persistência (Simulada):**
    * O estado dos assentos desabilitados e as localizações das portas são armazenados em campos ocultos (`hidden input`) para serem enviados a um script de backend (`salvar_layout.php`) ao submeter o formulário. [cite: 91, 92, 93]
    * O nome do mapa também é enviado para o backend. [cite: 87]

## Como Funciona

O sistema é construído com uma combinação de PHP, HTML, CSS e JavaScript:

1.  **PHP:**
    * Define a configuração inicial do layout, como o número total de assentos e quais assentos são candidatos a ter uma porta ao lado. [cite: 1, 4, 5, 8, 9]
    * Renderiza a estrutura HTML inicial das tabelas de assentos. [cite: 97, 98, 99, 100, 102, 103]
    * Preenche os valores iniciais para o nome do mapa e os dados de assentos desabilitados/portas (se houver). [cite: 11, 88, 92, 93]

2.  **HTML:**
    * Estrutura a página, incluindo o contêiner do ônibus, as tabelas de assentos, o formulário para o nome do mapa, os campos ocultos para dados e a legenda. [cite: 91, 97, 102, 121]

3.  **CSS:**
    * Estiliza todos os elementos visuais:
        * O contêiner do ônibus, incluindo uma imagem de fundo. [cite: 22]
        * A aparência dos assentos em diferentes estados (habilitado, desabilitado, ocupado, espaço vazio). [cite: 35, 37, 39, 40]
        * O menu de contexto e a legenda. [cite: 70, 56]
        * O layout de duas tabelas para simular os lados do ônibus com um corredor. [cite: 24, 25, 28]

4.  **JavaScript:**
    * Manipula toda a interatividade do editor no lado do cliente:
        * **Adicionar/Remover Assentos:** Modifica dinamicamente o DOM para adicionar ou remover células de assento (TDs) e atualiza seus atributos. [cite: 130, 131, 132, 133, 134, 137, 138, 139, 140, 141, 203, 204]
        * **Menu de Contexto:** Controla a exibição e as ações do menu de contexto para os assentos. [cite: 144, 173, 176]
        * **Status do Assento:** Alterna as classes CSS de um assento e atualiza a lista de assentos desabilitados. [cite: 195, 197, 198, 200]
        * **Gerenciamento de Portas:** Adiciona ou remove visualmente as fileiras de portas (TRs) e atualiza os dados das portas. [cite: 183, 184, 189, 190, 192, 193]
        * **Renomeação de Assentos:** Permite ao usuário inserir um novo número para o assento através de um `prompt`. [cite: 207, 208]
        * **Atualização dos Inputs Ocultos:** Garante que os dados mais recentes sobre assentos desabilitados e posições das portas sejam refletidos nos campos `hidden input` antes do envio do formulário. [cite: 153, 194]
        * **Interação com Botões (+/-):** Os botões "+" e "-" dentro de cada célula permitem adicionar um assento a um espaço vazio ou transformar um assento existente em um espaço vazio, respectivamente. [cite: 17, 130, 137]

## Estrutura do Layout

* O layout do ônibus é renderizado em um `div` wrapper (`#layout_onibus_wrapper`). [cite: 22]
* Dentro deste wrapper, duas tabelas (`#tabela-esquerda` e `#tabela-direita`) representam os assentos de cada lado do corredor. [cite: 24, 97, 102]
* A imagem de fundo `images/img-onibus-sem-motorista.png` é usada para dar a forma visual do ônibus. [cite: 22]
* A legenda e o botão de salvar são posicionados para fácil acesso. [cite: 121, 128]

## Para Utilizar

1.  Clone o repositório.
2.  Certifique-se de ter um servidor web com suporte a PHP (ex: Apache, Nginx).
3.  Coloque os arquivos no diretório do seu servidor web.
4.  Acesse o arquivo principal (provavelmente `index.php` ou o nome do arquivo fornecido) através do seu navegador.
5.  Crie um arquivo `salvar_layout.php` para processar os dados do formulário enviados via POST. Este script receberá:
    * `nome_mapa`: O nome do layout. [cite: 87]
    * `poltronas_desabilitadas`: Um JSON string com os números dos assentos desabilitados. [cite: 92]
    * `door_locations`: Um JSON string com as localizações das portas. [cite: 93]

## Observações

* O código PHP define um layout inicial com 60 assentos distribuídos em 15 fileiras. [cite: 1, 5]
* A lógica para assentos "ocupados" está presente no CSS [cite: 39] e no PHP (ao verificar `status === 'ocupada'` para botões de porta [cite: 111]), mas a interface de edição principal não parece modificar assentos para este estado, focando em "habilitado" e "desabilitado".
* O script `salvar_layout.php` não está incluído e precisaria ser implementado para armazenar os dados do layout (por exemplo, em um banco de dados ou arquivo).# mapa_onibus
