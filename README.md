pip install Flask Flask-SQLAlchemy
projet
    /static
        /css
        /images
    /templates
        base.html
        index.html
    app.py
    from flask import Flask, render_template
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///boutique.db'
db = SQLAlchemy(app)

class Produit(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    nom = db.Column(db.String(80), nullable=False)
    prix = db.Column(db.Float, nullable=False)
    description = db.Column(db.Text, nullable=True)

@app.route('/')
def index():
    produits = Produit.query.all()
    return render_template('index.html', produits=produits)

if __name__ == '__main__':
    app.run(debug=True)
