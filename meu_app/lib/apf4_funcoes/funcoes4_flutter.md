1. O que são rotas anônimas em Flutter e como elas funcionam?

As rotas anônimas (Anonymous Routes) são rotas criadas diretamente no momento da navegação, sem possuir um nome definido.

Em vez de registrar previamente uma rota, cria-se a tela que será aberta utilizando o widget MaterialPageRoute.

A navegação acontece através do Navigator, que mantém uma pilha (Stack) de telas.

Quando uma nova tela é aberta:

ela é colocada no topo da pilha;
a tela anterior permanece em memória;
ao voltar, a tela do topo é removida da pilha.
Funcionamento
Tela A
   ↓
Navigator.push()
   ↓
Tela B

Quando o usuário pressiona "Voltar":

Tela A ← Navigator.pop() ← Tela B
Exemplo
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => SegundaTela(),
  ),
);

Nesse exemplo:

Navigator.push() adiciona uma nova tela.
MaterialPageRoute cria uma rota.
builder informa qual tela será construída.
2. Quais métodos do Navigator são comumente utilizados e por quê?

O Navigator possui diversos métodos.

Navigator.push()

Abre uma nova tela.

Navigator.push(
  context,
  MaterialPageRoute(builder: (_) => SegundaTela()),
);

Uso:

navegar para outra página;
manter possibilidade de voltar.
Navigator.pop()

Fecha a tela atual.

Navigator.pop(context);

Muito utilizado em:

botão Voltar;
finalizar formulários;
fechar diálogos.
Navigator.pushReplacement()

Substitui a tela atual.

Navigator.pushReplacement(
  context,
  MaterialPageRoute(builder: (_) => Home()),
);

Uso:

Login → Home
Splash → Home

O usuário não consegue voltar para a tela anterior.

Navigator.pushNamed()

Navega usando uma rota nomeada.

Navigator.pushNamed(context, "/home");
Navigator.pushNamedAndRemoveUntil()

Remove várias telas da pilha.

Navigator.pushNamedAndRemoveUntil(
  context,
  "/home",
  (route) => false,
);

Muito utilizado após login.

Navigator.popUntil()

Volta até determinada tela.

Navigator.popUntil(
  context,
  ModalRoute.withName("/home"),
);
Navigator.canPop()

Verifica se existe tela anterior.

if (Navigator.canPop(context)) {
    Navigator.pop(context);
}
3. Qual a função do Navigator.push() na navegação com rotas anônimas?

O método push() adiciona uma nova rota na pilha de navegação.

Ele:

cria uma nova tela;
empilha essa tela;
mantém a tela anterior na memória.

Exemplo:

Navigator.push(
  context,
  MaterialPageRoute(
    builder: (_) => SegundaTela(),
  ),
);

Fluxo:

Home

↓

push()

↓

Segunda Tela

Depois:

pop()

↓

Home
4. Quais as vantagens e desvantagens de usar rotas anônimas?
Vantagens

✔ Simples.

✔ Fácil para projetos pequenos.

✔ Não precisa registrar rotas.

✔ Boa para poucas telas.

✔ Permite passar objetos diretamente.

Exemplo:

Navigator.push(
  context,
  MaterialPageRoute(
    builder: (_) => Produto(produto),
  ),
);
Desvantagens

✘ Código espalhado.

✘ Difícil manutenção.

✘ Navegação menos organizada.

✘ Pouco reutilizável.

✘ Em projetos grandes torna-se difícil localizar todas as navegações.

5. O que são rotas nomeadas em Flutter e como elas funcionam?

Rotas nomeadas são telas registradas previamente através de um nome.

Cada tela recebe uma String.

Exemplo:

"/"

"/login"

"/home"

"/perfil"

Depois basta chamar:

Navigator.pushNamed(
    context,
    "/perfil",
);

O Flutter procura essa rota no MaterialApp.

6. Como posso navegar para uma rota nomeada específica?

Utiliza-se:

Navigator.pushNamed(
    context,
    "/cadastro",
);

Também é possível enviar parâmetros.

Navigator.pushNamed(
  context,
  "/produto",
  arguments: produto,
);
7. Quais as vantagens de usar rotas nomeadas em relação às rotas anônimas?
Organização

Todas as telas ficam centralizadas.

Reutilização

Não precisa criar MaterialPageRoute toda vez.

Facilidade de manutenção

Caso o nome da tela mude:

antes:

Navigator.push(...)

Navigator.push(...)

Navigator.push(...)

depois:

"/home"

Altera apenas uma vez.

Escalabilidade

Ideal para sistemas grandes.

Melhor leitura
Navigator.pushNamed(context, "/perfil");

É mais legível do que:

Navigator.push(
context,
MaterialPageRoute(
builder: (_) => Perfil()),
);
8. Como posso definir rotas nomeadas em meu aplicativo Flutter?

Dentro do MaterialApp.

MaterialApp(

initialRoute: "/",

routes: {

"/": (context) => Home(),

"/login": (context) => Login(),

"/perfil": (context) => Perfil(),

},

);

Agora basta chamar.

Navigator.pushNamed(
context,
"/perfil",
);
9. Como posso acessar os parâmetros passados em uma rota nomeada?

Primeiro envia-se.

Navigator.pushNamed(
context,
"/produto",
arguments: "Notebook",
);

Na tela destino:

final nome = ModalRoute.of(context)!
    .settings
    .arguments as String;

Agora a variável possui:

Notebook

Também pode enviar objetos.

arguments: usuario

Depois:

final usuario =
ModalRoute.of(context)!
.settings.arguments as Usuario;
10. Como posso tornar os parâmetros opcionais em uma rota nomeada?

Basta verificar se existe argumento.

final args =
ModalRoute.of(context)?.settings.arguments;

Depois:

if(args != null){

}

Ou:

final nome =
ModalRoute.of(context)
?.settings.arguments
as String?;

Assim:

se existir → usa;
se não existir → recebe null.

Também é possível definir valor padrão.

final nome =
ModalRoute.of(context)
?.settings.arguments
as String? ??
"Visitante";
11. Quais cuidados devo ter ao usar as rotas?

Alguns cuidados importantes:

evitar abrir muitas telas desnecessariamente;
sempre fechar telas quando necessário usando pop();
evitar nomes duplicados de rotas;
validar parâmetros antes de utilizá-los;
utilizar constantes para nomes das rotas;
evitar navegação dentro do método build();
manter a navegação organizada;
utilizar pushReplacement() quando não houver necessidade de voltar.
12. Quais as boas práticas ao usar rotas em Flutter?

As principais boas práticas são:

criar um arquivo exclusivo para rotas;
usar constantes para nomes das rotas;
organizar telas por pastas;
evitar código duplicado;
validar argumentos;
utilizar rotas nomeadas em projetos grandes;
utilizar rotas anônimas apenas quando fizer sentido;
documentar a navegação;
utilizar pushReplacement() para login;
utilizar pushNamedAndRemoveUntil() após autenticação.

Exemplo:

class AppRoutes {

static const home="/";

static const login="/login";

static const perfil="/perfil";

}

Depois:

Navigator.pushNamed(
context,
AppRoutes.perfil,
);
13. Exemplo de galeria navegando entre imagens usando rotas anônimas
Objetivo

Criar uma galeria simples em que a primeira tela exibe miniaturas de imagens. Ao tocar em uma imagem, o aplicativo abre uma segunda tela utilizando rotas anônimas, mostrando a imagem em tamanho maior.

Código
main.dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    debugShowCheckedModeBanner: false,
    home: Galeria(),
  ));
}

class Galeria extends StatelessWidget {
  final List<String> imagens = [
    "assets/img1.jpg",
    "assets/img2.jpg",
    "assets/img3.jpg",
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Galeria")),
      body: GridView.builder(
        itemCount: imagens.length,
        gridDelegate:
            SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: 2,
        ),
        itemBuilder: (context, index) {
          return GestureDetector(
            onTap: () {
              Navigator.push(
                context,
                MaterialPageRoute(
                  builder: (_) => TelaImagem(imagens[index]),
                ),
              );
            },
            child: Padding(
              padding: EdgeInsets.all(8),
              child: Image.asset(imagens[index]),
            ),
          );
        },
      ),
    );
  }
}

class TelaImagem extends StatelessWidget {
  final String imagem;

  TelaImagem(this.imagem);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Imagem")),
      body: Center(
        child: Image.asset(imagem),
      ),
    );
  }
}
Funcionamento
A tela inicial exibe uma grade com imagens.
O usuário toca em uma imagem.
Navigator.push() cria uma rota anônima usando MaterialPageRoute.
A tela TelaImagem recebe o caminho da imagem e a exibe em tamanho maior.
Ao pressionar o botão de voltar, Navigator.pop() retorna à galeria.
14. Crie um fluxo com várias telas, passando pelos times brasileiros usando rotas nomeadas e parâmetros
Objetivo

Criar um aplicativo com:

Tela Inicial
Lista de Times
Tela de Detalhes

Utilizando rotas nomeadas e parâmetros.

Estrutura
Home
   ↓
Lista de Times
   ↓
Detalhes do Time
main.dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      initialRoute: '/',
      routes: {
        '/': (context) => HomePage(),
        '/times': (context) => TimesPage(),
        '/detalhes': (context) => DetalhesPage(),
      },
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Início')),
      body: Center(
        child: ElevatedButton(
          child: Text('Ver Times'),
          onPressed: () {
            Navigator.pushNamed(context, '/times');
          },
        ),
      ),
    );
  }
}

class TimesPage extends StatelessWidget {
  final List<String> times = [
    'Flamengo',
    'Palmeiras',
    'Corinthians',
    'São Paulo',
    'Grêmio',
    'Internacional',
    'Cruzeiro',
    'Atlético Mineiro',
    'Fluminense',
    'Botafogo'
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Times Brasileiros')),
      body: ListView.builder(
        itemCount: times.length,
        itemBuilder: (context, index) {
          return ListTile(
            title: Text(times[index]),
            trailing: Icon(Icons.arrow_forward),
            onTap: () {
              Navigator.pushNamed(
                context,
                '/detalhes',
                arguments: times[index],
              );
            },
          );
        },
      ),
    );
  }
}

class DetalhesPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final String time =
        ModalRoute.of(context)!.settings.arguments as String;

    return Scaffold(
      appBar: AppBar(title: Text(time)),
      body: Center(
        child: Text(
          'Bem-vindo à página do $time!',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
Funcionamento do fluxo
O aplicativo inicia na HomePage.
Ao clicar em "Ver Times", o usuário navega para '/times'.
A tela TimesPage exibe uma lista com clubes brasileiros.
Ao selecionar um clube, Navigator.pushNamed() envia o nome do time pelo parâmetro arguments.
A DetalhesPage recupera o argumento com ModalRoute.of(context)!.settings.arguments e exibe o nome do clube selecionado.
O botão de voltar retorna para a tela anterior, mantendo o fluxo de navegação organizado por meio de rotas nomeadas