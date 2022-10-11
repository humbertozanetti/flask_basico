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
