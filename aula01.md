### Aula 01 - "Hello World" em Flask

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


