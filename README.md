# Processo de Avaliação

Projeto para avaliar conhecimentos em Flutter.

## Proposta
Desenvolver app "Livro de memórias". Este aplicativo deve permitir que o usuário registre **Memórias**, adicione **Fotos** e inclua as **Pessoas** presentes nas Memórias. Todos os dados serão salvos localmente, exceto as fotos, que serão hospedadas no Imgur.

## Requisitos
- Os dados devem ser salvos em um banco de dados local, utilizando a biblioteca [moor](https://moor.simonbinder.eu/). Recomenda-se o uso de [DAO's](https://moor.simonbinder.eu/docs/advanced-features/daos/).
- Usar [named routes](https://flutter.dev/docs/cookbook/navigation/named-routes).
- As imagens devem ser hospedadas/armazenadas usando a [API do Imgur](https://apidocs.imgur.com/).
- **Telas**:
  - a tela principal deve conter a listagem das **Memórias** já registradas.
  - tela com a listagem das pessoas registradas.
  - tela para visualizar os detalhes de uma **Memória**, que deve exibir:
       - título, data, local, descrição.
       - as **Fotos** relacionadas.
       - as **Pessoas** presentes (ao "clicar" em uma Pessoa, o app deve abrir a tela de detalhes dessa Pessoa).
  - tela para visualizar os detalhes de uma **Pessoa**, que deve exibir:
      - nomes, data de nascimento, imagem de peril, descrição/comentário.
      - as **Memórias** nas quais essa Pessoa está presente (ao "clicar" em uma Memória, o app deve abrir a tela de detalhes dessa Memória).
  - tela para registrar uma nova **Memória**.
  - tela para registrar uma nova **Pessoa**.

  

### Entidades do Banco de Dados
#### Entidades
- **Memória**:
  - \<String> título
  - \<DateTime> data
  - \<String> descrição (opcional)
  - \<String> local (opcional)
- **Foto**:
  - \<String> url da imagem
- **Pessoa**:
  - \<String> primeiro nome
  - \<String> sobrenome (opcional)
  - \<DateTime> data de nascimento (opcional)
  - \<String> descrição/comentário (opcional)
  - \<String> url da imagem de perfil (opcional)

#### Relacionamentos
- Uma **Memória** pode ter várias **Fotos** relacionadas a ela, mas uma **Foto** só pode estar relacionada a uma **Memória**.
- Muitas **Pessoas** podem estar presentes em uma **Memória**, e uma **Pessoa** pode estar presente em várias **Memórias**.

## Avaliação
O foco deste projeto é avaliar o uso de REST APIs, o uso da biblioteca Moor, e a organização e modularidade do código. Design de UI/UX não é um fator determinante na avaliação, no entanto a interface deve ser minimamente utilizável.

## Observações e Dicas
- A sessão de **Requisitos** estabelece as definições mínimas para este projeto. Você é livre para acrescentar mais telas, funcionalidades ou modelos no banco de dados.
- As telas descritas acima não precisam necessariamente estar em rotas separadas. Por exemplo, você pode colocar a tela de listagem de memórias e de listagem de pessoas em um mesmo [PageView](https://api.flutter.dev/flutter/widgets/PageView-class.html).
- Uma boa biblioteca para exibir imagens da web é a [cached_network_image](https://pub.dev/packages/cached_network_image).
- **Por onde começar?** 
  - Primeiramente, aprenda a usar o Moor por meio da documentação e de uns [tutoriais](https://www.youtube.com/playlist?list=PLB6lc7nQ1n4glsY1J0R6jWirqtURKClz7).
  - Faça telas de protótipo que lhe permitam inserir e exibir os dados.
  - Use valores fixos para os dados que você ainda não tiver. Por exemplo, enquanto você ainda não implementar métodos para inserir e buscar imagens do Imgur, todas as Fotos poderiam ter a URL http://www.pudim.com.br/pudim.jpg
  - Foque primeiro nas funcionalidades (banco de dados, API, etc), pois é a parte mais importante do projeto, e deixe o design por último.
- Você com certeza vai precisar passar parâmetros entre rotas. Para lhe poupar horas de busca no StackOverflow, aqui está um exemplo de código:


```dart
// Declarar Widget:
class TelaDetalhesCarro extends StatelessWidget {
    final Carro carro;

    TelaDetalhesCarro({{Key key, this.carro}}) : super(key: key);
    // ...
    // ...
}

// Na definicão dos nomes das rotas:
{
    // ...
    '/carros/detalhes': (BuildContext context) => TelaDetalhesCarro(data: ModalRoute.of(context).settings.arguments),
    // ...
}

// Na hora de chamar a rota:
Carro meuCamaroAmarelo;
// ...
// ...
Navigator.of(context).pushNamed('/carros/detalhes', arguments: meuCamaroAmarelo);

```