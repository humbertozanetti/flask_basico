# Utilizando HTML

Até agora tinhamos visto apenas as funções gerarem strings, mas sem usar HTML, que é o padrão de composição de informações na web.
Caro seja necessário, no Python podemos gerar uma string que possua a composição HTML. No momento em que o navegador "renderize" a página, o código HTML será corretamente interpretado.
 
```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def index():
    return '<html><body><h1>Hello World</h1></body></html>'

if __name__ == '__main__':
    app.run(debug=True)
```

Outro exemplo:

```
from flask import Flask
app = Flask(__name__)
  
@app.route('/')
def index():
  return '<h1>Hello World!</h1>'
    
@app.route('/user/<name>')
def user(name):
  return '<h1>Hello, %s!</h1>' % name
 
if __name__ == '__main__':
    app.run(debug=True)
```

Mesmo podemos "gerar" HTML pelo Python, o ideal é que utilizemos **templates**, que seriam as páginas HTML melhores estruturadas e trabalhadas, interagindo com nosso código-fonte. Isso faz com que possamos trabalhar **separadamente** com o HTML e o código-fonte.
Vamos fazer um exemplo utilizando a uma página HTML simples, podendo nomeá-la de "index.html". Crie uma pasta chamada **template** para colocar todas as páginas HTML. **O USO DESSA PASTA É OBRIGATÓRIO PARA O FLASK!!!**.

```
<html>
    <head>
    </head>
    <body>
        <h1>Hello World!!!</h1>
    </body>
</html>
```

Para utilizar os templates precisamos importar a classe **render_template**.

```
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=True)
```
Uma das maiores funcionalidades do Flask é conseguir interagir com o HTML através de varíaveis existentes em **marcadores dupla chaves {{ }}**. O exemplo a seguir mostra como podemos fazer um valor vindo da URL para o HTML. Crie um "user.html" com o código a seguir:

```
<html>
    <head>
    </head>

    <body>
        <h1>Hello {{ nome }}!!!</h1>
    </body>
</html>
```

Note que existe uma marcação **nome**, que será referência para passar o valor do código Python para o HTML. E a variável **nome_user** é o valor passado pela URL.

```
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/user/<nome_user>')
def user(nome_user):
    return render_template('user.html', nome=nome_user)

if __name__ == '__main__':
    app.run(debug=True)
```

