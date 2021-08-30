# Flask

## flask routes
### flask-start
```
from flask import Flask

app = Flask(__name__)

# creating route
@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"

if __name__ == "__main__":
    app.run(debug=True)
```

#### Run
```
python your_directory.py
```

### render_template, redirect and url_for
```
from flask import Flask, render_template, redirect, url_for

app = Flask(__name__)

@app.route("/")
def home():
    return render_template("home.html")


@app.route("/add")
def add():
    return render_template("add.html")


@app.route("/update")
def update():
    return render_template("update.html")


@app.route("/delete")
def delete():
    return redirect(url_for('home'))


if __name__ == "__main__":
    app.run(debug=True)
```

### Request Method
```
from flask import Flask, render_template, redirect, url_for, request

@app.route("/add", methods=['GET', 'POST'])
def add():
    print(request.method)
    return render_template("add.html")
```


### Request Form
```
HTML
<form method="post" action="{{ url_for('add') }}">
    <div class="input_fields">
        <input type="text" name="name" id="name" placeholder="Name" required><br>
        <input type="password" name="password" id="password" placeholder="Password" required><br>
        <input type="email" name="email" id="email" placeholder="Email" required><br>
    </div>
    <button class="rounded_gradiant_md_btn">
        Submit
    </button>
</form>

FLASK
@app.route("/add", methods=['GET', 'POST'])
def add():
    if request.method == 'POST':
        name = request.form['name']
        password = request.form['password']
        email = request.form['email']
        new_data = {"name": name, "password": password, "email": email}
        print(new_data)
    return render_template("add.html")
```

### Request Argument
```
HTML
<form method="post" action="{{ url_for('add', data = 'data') }}">
    <div class="input_fields">
        <input type="text" name="name" id="name" placeholder="Name" required><br>
        <input type="password" name="password" id="password" placeholder="Password" required><br>
        <input type="email" name="email" id="email" placeholder="Email" required><br>
    </div>
    <button class="rounded_gradiant_md_btn">
        Submit
    </button>
</form>

FLASK
@app.route("/add", methods=['GET', 'POST'])
def add():
    if request.method == 'POST':
        print(request.args['data'])
        return redirect(url_for('home'))
    return render_template("add.html")
```

------------------------

### API Requests
```
import requests

response = requests.get("https://jsonplaceholder.typicode.com/users", params={"email":'Shanna@melissa.tv'})
response_data = response.json()
print(response_data)
```





