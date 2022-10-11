# Aula 01 - "Hello World" em Flask

Para trabalhar com o Flask, devemos utilizar uma importação e apontar um objeto do tipo Flask:

```
from flask import Flask
app = Flask(__name__)
```

Toda a base do Flask funciona pelo conceito de **rotas**. Rotas são "caminhos" que defimos na URL que apontam qual função deverá ser chamada.
Por exemplo, se queremos ir para a **raiz** ou **página principal** o caminho da rota é **'/'**.

```
@app.route('/')
def hello_world():
    return 'Hello World'
```
Note que a função que temos um **decorator**, que é uma propriedade em Python que restutura propriedades de uma função. Nesse caso do decorator **@app.rout** faz com que a função fique vinculada a uma rota.
Agora, precisamos definir a chamada de nossa aplicação, quando for executada com o trecho:
```
if __name__ == '__main__':
    app.run(debug=True)
```
Essa definição é a melhor maneira de usar a aplicação, pois podemos ver o resultado das ações através de "refresh" da nossa página.
Supondo que nosso arquivo se chama **app.py** basta fazer o comando **python app.py** dentro da pasta do projeto para que ele execute.
O código completo está abaixo:

```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World'

if __name__ == '__main__':
    app.run(debug=True)
```

## Usando e entenddo a passagem de valores via web

Há 2 meios de passar valores via web, sendo um o **GET** e o outro **POST**:
- GET: os valores são visíveis na URL;
- POST: os valores **não** são visíveis na URL.
Faremos um exemplo de como, por meio de GET, podemos usar valores passados e atribuir em variáveis.
```
from flask import Flask
app = Flask(__name__)

@app.route('/hello/<name>')
def hello_name(name):
    return 'Hello %s!' % name

if __name__ == '__main__':
    app.run(debug=True)
```
Notem que nossa rota mudou, agora temos um caminho composto por **/hello/**. O valor passado após a rota será o **valor** passado.
Ao acessar a rota **http://127.0.0.1:5000/hello/Luke**, veremos que **Luke** para atribuído à variável **name**, que é o parâmetro de entrada da função.

## Definição de tipos e problemas na URL

Para bloquear tipos indesejados de valores, pode definir os **tipos dos valores** a serem passados:
```
from flask import Flask
app = Flask(__name__)

@app.route('/blog/<int:postID>')
def show_blog(postID):
    return 'Blog número %d' % postID

@app.route('/rev/<float:revNo>')
def revision(revNo):
    return 'Revisão número %f' % revNo
    
if __name__ == '__main__':
    app.run(debug=True)
```
Se tentar passar um valor não correspondente em qualquer uma das rotas, a página não será encontrada.

Como boa prática muitas vezes colocamos as rotas para serem acessadas por uma **/** ou duas. Por exemplo:
```
from flask import Flask
app = Flask(__name__)


# NOTE: somente a URL '/flask' funciona
@app.route('/flask')
def hello_flask():
    return 'Hello Flask'

# NOTE: ambas URLs '/python' e '/python/' funcionam
@app.route('/python/')
def hello_python():
    return 'Hello Python'
   
if __name__ == '__main__':
    app.run(debug=True)
```

### Exercício

Faça um programa que tenha duas rotas. Uma rota leva para o **ADMIN** e outro para um **GUEST**. A rota **raiz** irá receber o valor **nome**. Se form digitado **ADMIN**, a rota será direcionada para uma função que irá imprimir **"Olá ADMIN**. Agora, se for digitado algum nome, será encaminhado para outra função que irá imprimir **Olá Fulano, você é GUEST**.
