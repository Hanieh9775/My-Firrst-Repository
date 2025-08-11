from flask import Flask, request, render_template_string

app = Flask(__name__)

HTML_TEMPLATE = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Simple Web App</title>
</head>
<body>
    <h1>Simple Web Application</h1>
    <form method="post">
        <label for="name">Enter your name:</label>
        <input type="text" id="name" name="name" required>
        <button type="submit">Submit</button>
    </form>
    {% if name %}
        <h2>Hello, {{ name }}!</h2>
    {% endif %}
</body>
</html>
"""

@app.route("/", methods=["GET", "POST"])
def home():
    name = None
    if request.method == "POST":
        name = request.form.get("name")
    return render_template_string(HTML_TEMPLATE, name=name)

if __name__ == "__main__":
    app.run(debug=True)
