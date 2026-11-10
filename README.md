# 📖 Guia do Usuário — Dashboard de Vendas

Este manual explica **como configurar e usar a sincronização em nuvem** e **como funciona cada repartição da página** do sistema.

---

## ☁️ 1. Como Utilizar a Nuvem (Sincronização entre Celular e PC)

O sistema utiliza a API gratuita do **[JSONBin.io](https://jsonbin.io)** para armazenar suas vendas na nuvem. Dessa forma, qualquer venda cadastrada no computador aparece no celular e vice-versa, sem precisar instalar nada.

### Passo a Passo de Configuração:

1. **Criar Conta Gratuita:**
   - Acesse [jsonbin.io](https://jsonbin.io) e crie uma conta gratuita (pode usar o login com o Google ou GitHub).

2. **Criar a Base de Dados (Bin):**
   - No painel do JSONBin, vá na aba **Bins** e clique em **Create Bin** (ou ícone de `+`).
   - Na caixa de texto, apague tudo e digite apenas:
     ```json
     []
     ```
   - Clique em **Save Bin**.
   - Copie o **BIN ID** gerado (um código alfanumérico, ex: `6735e123ad19ca34f8123456`).

3. **Copiar a Chave de Acesso (API Key):**
   - No menu lateral do JSONBin, clique em **API Keys**.
   - Copie a sua **Master Key** (que começa com `$2a$10$...`) ou crie uma Access Key com permissão de leitura e gravação.

4. **Conectar no Dashboard:**
   - Abra a página do dashboard no navegador.
   - No topo direito, clique no botão com ícone de nuvem (<i data-lucide="cloud-cog"></i> **Configurar Conexão Nuvem**).
   - Cole o seu **BIN ID** e a sua **Master Key**.
   - Clique em **Salvar**.

### Como a Sincronização Funciona:
* **Automática:** Ao cadastrar, editar ou excluir qualquer venda, o sistema grava instantaneamente no cache local do aparelho e dispara a atualização para a nuvem.
* **Status no Cabeçalho:**
  * 🟢 **Nuvem Conectada / Salvo na Nuvem**: Dados salvos e sincronizados com sucesso.
  * 🟡 **Sincronizando...**: Gravando ou baixando dados da nuvem.
  * ⚪ **Modo Local / Offline**: O sistema opera usando o armazenamento do próprio navegador caso não haja conexão ou chaves configuradas.
* **Botão Recarregar (<i data-lucide="refresh-cw"></i>):** Localizado no cabeçalho, força a busca dos lançamentos mais recentes salvos na nuvem (ótimo para atualizar o celular após fazer lançamentos no PC).

---

## 🖥️ 2. Como Funciona Cada Repartição da Página

---

### A. Cabeçalho (Header Superior)
Fica fixo no topo da tela para navegação rápida:
* **Nome do Usuário (Editável):** Exibe o nome do proprietário das vendas (padrão *"Minhas Vendas"*). Ao clicar nele ou no ícone de lápis (`✏️`), você pode digitar seu próprio nome e pressionar <kbd>Enter</kbd>. Fica salvo no cache local do seu navegador.
* **Indicador de Nuvem:** Exibe em tempo real o status da conexão (*Modo Local*, *Sincronizando* ou *Nuvem Conectada*).
* **Botão Atualizar (<i data-lucide="refresh-cw"></i>):** Recarrega os dados da nuvem na hora.
* **Botão Conexão Nuvem (<i data-lucide="cloud-cog"></i>):** Abre o modal para inserir ou alterar o BIN ID e a chave do JSONBin.
* **Botão Tema Escuro/Claro (<i data-lucide="moon"></i> / <i data-lucide="sun"></i>):** Alterna o visual entre modo escuro (Dark Mode) e modo claro.
* **Botão Nova Venda (Desktop):** Abre o formulário de cadastro de vendas (atalho: tecla <kbd>N</kbd>).

---

### B. Barra de Período (Data de Referência das Estatísticas)
Localizada logo abaixo do cabeçalho, controla o dia base para todos os cálculos do painel:
* **Campo de Seleção de Data:** Permite escolher qualquer dia. Todas as estatísticas (vendas do dia, faturamento acumulado no mês, dias úteis restantes e meta diária) são recalculadas considerando o cenário **até aquela data selecionada**.
* **Botão "Hoje":** Redefine a data de referência imediatamente para o dia atual em tempo real.
* **Badge de Status:**
  * 🟢 *Hoje (Tempo Real)*: Acompanhamento ao vivo das vendas atuais.
  * 🟡 *Histórico até DD/MM/AAAA*: Auditoria retroativa de um dia passado.
  * 🟣 *Projeção até DD/MM/AAAA*: Simulação de datas futuras.

---

### C. Seção de Metas & Remuneração
Calcula automaticamente a remuneração com base nas regras comerciais e trabalhistas:
* **Seletores de Alvo Mensal:** Botões para alternar o objetivo do mês entre:
  * **110k** → Comissão de **1,5%**
  * **120k** → Comissão de **2,0%**
  * **130k** → Comissão de **2,1%**
  * **140k** → Comissão de **2,5%**
  *(Vendas abaixo de 110k recebem a comissão base de 1,0%)*
* **Card "Total no Bolso (Líquido)":** Soma o Salário Base CLT Líquido (R$ 1.499,42, já com desconto de 7,5% do INSS) com a comissão total acumulada no mês até a data de referência.
* **Card "Meta Diária Reajustada":** 
  * Calcula os dias úteis restantes no mês (escala de **Segunda a Sábado**, excluindo domingos e feriados nacionais móveis e fixos).
  * Divide o valor que falta faturar pelos dias úteis que restam.
  * **Badge de Ritmo:** Informa se a meta diária foi *aliviada* (porque você vendeu mais que o esperado nos dias anteriores) ou se *subiu* (necessidade de acelerar o ritmo diário).
* **Card "Falta Faturar":** Mostra exatamente quantos reais faltam para atingir a meta mensal selecionada.
* **Card "Próximo Degrau":** Indica qual é o próximo percentual de comissão a ser alcançado e quantos reais faltam para destravá-lo.
* **Barra de Progresso com 4 Degraus:** Mostra visualmente a porcentagem atingida em relação ao alvo e destaca os degraus já batidos (110k, 120k, 130k, 140k) com cor verde.

---

### D. Cards Principais de Vendas (KPIs)
Quatro cartões com métricas diretas:
1. **Vendas na Data:** Faturamento total realizado na data selecionada, quantidade de pedidos e se a meta daquele dia específico foi batida.
2. **Faturamento Mês:** Faturamento total acumulado desde o primeiro dia do mês até a data selecionada.
3. **Ticket Médio:** Valor médio faturado por lançamento no mês analisado.
4. **Lançamentos:** Quantidade total de vendas registradas no mês até a data.

---

### E. Seção de Gráficos Visuais
Dois gráficos dinâmicos para acompanhar a performance:
* **Evolução Diária (Linha):** Mostra as vendas dia a dia nos **15 dias anteriores** à data de referência selecionada.
* **Comparativo Mensal (Barras):** Mostra o total faturado mês a mês nos **últimos 6 meses** até o mês analisado.

---

### F. Histórico de Lançamentos & Filtros
Área onde ficam listadas todas as vendas registradas:
* **Barra de Busca (<kbd>/</kbd>):** Digite o nome do produto ou descrição para filtrar instantaneamente.
* **Filtro por Mês:** Permite visualizar lançamentos de meses anteriores.
* **Filtro por Pagamento:** Filtra por Pix, Cartão de Crédito, Cartão de Débito, Dinheiro ou A Definir.
* **Opção "Até a data selecionada":** Checkbox que limita a tabela para exibir apenas os lançamentos feitos até o dia configurado no seletor de data superior.
* **Botão "Exportar CSV":** Baixa uma planilha com todos os lançamentos atualmente visíveis na tela (formatada em ponto-e-vírgula e UTF-8 para abrir perfeitamente no Excel brasileiro).
* **Modo Tabela (Desktop):** Exibe colunas com Data, Descrição, Forma de Pagamento, Valor e botões de **Editar** (<i data-lucide="edit-3"></i>) e **Excluir** (<i data-lucide="trash-2"></i>).
* **Modo Cartões (Celular):** Exibe as vendas em formato de cartões limpos estilo extrato bancário, com ações rápidas de toque.
* **Totalizador no Rodapé:** Mostra quantos registros estão visíveis e a soma total do valor filtrado.

---

### G. Modais e Botão Flutuante
* **Botão Flutuante (+) no Celular:** Fica fixo no canto inferior direito para permitir adicionar uma nova venda com um toque.
* **Modal Cadastrar / Editar Venda:** Permite preencher Descrição/Produto, Valor (R$), Data da venda e Forma de Pagamento.
* **Modal de Confirmação de Exclusão:** Protege contra cliques acidentais ao tentar remover uma venda.
