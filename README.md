## Desafio 01 - Criando um hook de carrinho de compras
***
#### Desafio concluido para o curso de Reactjs da Rocketseat.
### Sobre o desafio
Nesse desafio, você deverá criar uma aplicação para treinar o que aprendeu até agora no ReactJS

Essa será uma aplicação onde o seu principal objetivo é criar um hook de carrinho de compras. Você terá acesso a duas páginas, um componente e um hook para implementar as funcionalidades pedidas nesse desafio:
- Adicionar um novo produto ao carrinho;
- Remover um produto do carrinho;
- Alterar a quantidade de um produto no carrinho;
- Cálculo dos preços sub-total e total do carrinho;
- Validação de estoque;
- Exibição de mensagens de erro;
- Entre outros.

#### Rotas da aplicação
Perceba que ele iniciou uma fake API com os recursos /stock e /products em localhost na porta 3333 a partir das informações do arquivo server.json localizado na raiz do seu projeto. Acessando essas rotas no seu navegador, você consegue ver o retorno das informações já em JSON:
Para acessar a listagem de todos os produtos e estoque, basta realizar uma requisição GET nas rotas /products e /stock respectivamente. Para acessar os dados de um único item utilize os route params, exemplo: /products/1 e /stock/1 para acessar os dados do produto e estoque do produto de id 1, respectivamente.


### O que devo editar na aplicação?

Com o template já clonado, as depêndencias instaladas e a [fake API rodando], você deve completar onde não possui código com o código para atingir os objetivos de cada teste. Os documentos que devem ser editados são:

- [src/components/Header/index.tsx]
- [src/pages/Home/index.tsx]
- [src/pages/Cart/index.tsx]
- [src/hooks/useCart.tsx]
- 
### components/Header/index.tsx
Você deve renderizar os produtos buscados da fake API em tela com as informações de título, imagem, preço e quantidade adicionada ao carrinho. Por fim, é preciso implementar a funcionalidade de adicionar o produto escolhido ao carrinho ao clicar no botão ADICIONAR AO CARRINHO.
Nesse arquivo, temos três pontos importantes a serem implementados:
- cartItemsAmount: Deve possuir as informações da quantidade de cada produto no carrinho. Sugerimos criar um objeto utilizando reduce onde a chave representa o id do produto e o valor a quantidade do produto no carrinho. Exemplo: se você possuir no carrinho um produto de id 1 e quantidade 4 e outro produto de id 2 e quantidade 3, o objeto ficaria assim:
- loadProducts: Deve buscar os produtos da Fake API e formatar o preço utilizando o helper utils/format
- handleAddProduct: Deve adicionar o produto escolhido ao carrinho.

####  pages/Cart/index.tsx
Você deve renderizar uma tabela com a imagem, título, preço unitário, quantidade de unidades e preço subtotal de cada produto no carrinho. Além disso, também é preciso renderizar o preço total do carrinho. Por fim, é preciso implementar as funcionalidades dos botões de decrementar, incrementar e remover o produto do carinho.
Nesse arquivo, temos cinco pontos importantes a serem implementados:
- cartFormatted: Deve formatar o carrinho adicionando os campos priceFormatted (preço do produto) e subTotal (preço do produto multiplicado pela quantidade) ambos devidamente formatados com o utils/format.
- total: Deve possuir a informação do valor total do carrinho devidamente formatado com o utils/format.
- handleProductIncrement: Deve aumentar em 1 unidade a quantidade do produto escolhido ao carrinho.
- handleProductDecrement: Deve diminuir em 1 unidade a quantidade do produto escolhido ao carrinho, onde o valor mínimo é 1 (nesse caso o botão deve estar desativado).
- handleProductDecrement: Deve diminuir em 1 unidade a quantidade do produto escolhido ao carrinho, onde o valor mínimo é 1 (nesse caso o botão deve estar desativado).
- handleRemoveProduct: Deve remover o produto escolhido do carrinho.

#### hooks/useCart.tsx
Apesar de não retornar diretamente nenhuma renderização de elementos na interface como os outros arquivos, esse é o coração do desafio. Ele é responsável por:
- hook useCart;
- context CartProvider;
- manipular localStorage;
- exibir toasts.
- 
Então é aqui que você vai implementar as funcionalidades que serão utilizadas pelo restante do app. Os principais pontos são:
- cart: Deve verificar se existe algum registro com o valor @RocketShoes:cart e retornar esse valor caso existir. Caso contrário, retornar um array vazio.
- addProduct: Deve adicionar um produto ao carrinho. Porém, é preciso verificar algumas coisas.
- O valor atualizado do carrinho deve ser perpetuado no localStorage utilizando o método setItem.
- Caso o produto já exista no carrinho, não se deve adicionar um novo produto repetido, apenas incrementar em 1 unidade a quantidade;
- Verificar se existe no estoque a quantidade desejada do produto. Caso contrário, utilizar o método error da react-toastify com a seguinte mensagem:
    #### toast.error('Quantidade solicitada fora de estoque');

- Capturar utilizando trycatch os erros que ocorrerem ao longo do método e, no catch, utilizar o método error da react-toastify com a seguinte mensagem:
    #### toast.error('Erro na adição do produto');
- removeProduct: Deve remover um produto do carrinho. Porém, é preciso verificar algumas coisas:
- O valor atualizado do carrinho deve ser perpetuado no localStorage utilizando o método setItem.
- Capturar utilizando trycatch os erros que ocorrerem ao longo do método e, no catch, utilizar o método error da react-toastify com a seguinte mensagem:
    #### toast.error('Erro na remoção do produto');

- updateProductAmount: Deve atualizar a quantidade de um produto no carrinho. Porém, é preciso verificar algumas coisas:
- O valor atualizado do carrinho deve ser perpetuado no localStorage utilizando o método setItem.
- Se a quantidade do produto for menor ou igual a zero, sair da função updateProductAmount instantaneamente.
- Verificar se existe no estoque a quantidade desejada do produto. Caso contrário, utilizar o método error da react-toastify com a seguinte mensagem:
    #### toast.error('Quantidade solicitada fora de estoque');

- Capturar utilizando trycatch os erros que ocorrerem ao longo do método e, no catch, utilizar o método error da react-toastify com a seguinte mensagem:
    #### toast.error('Erro na alteração de quantidade do produto');