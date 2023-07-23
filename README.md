# Data-visualization-flask-code-
from flask import Flask, render_template
import plotly.graph_objs as go
import random

app = Flask(__name__)

@app.route('/')
def index():
    # Generate random data (e.g., 20 points)
    num_points = 20
    x_data = list(range(num_points))
    y_data = [random.randint(0, 100) for _ in range(num_points)]

    # Create a Plotly trace for the line chart
    trace = go.Scatter(x=x_data, y=y_data, mode='lines+markers')

    # Create a Plotly layout for the chart
    layout = go.Layout(title='Dynamic Data Visualization',
                       xaxis=dict(title='X-axis'),
                       yaxis=dict(title='Y-axis'))

    # Create the figure and render it as JSON
    figure = go.Figure(data=[trace], layout=layout)
    graph_json = figure.to_json()

    return render_template('index.html', graphJSON=graph_json)

if __name__ == '__main__':
    app.run(debug=True)
