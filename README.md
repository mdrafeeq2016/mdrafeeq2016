import dash
import dash_core_components as dcc
import dash_html_components as html
import pandas as pd

app = dash.Dash()

# Load the data
df = pd.read_csv('dashboard_data.csv')

# Create the dashboard layout
layout = html.Div([
    html.H1('Dashboard'),

    # Total punched orders
    html.Div([
        html.H3('Total Punched'),
        html.P(df['Total Punched'].sum()),
    ]),

    # Not confirmed orders
    html.Div([
        html.H3('Not Confirmed'),
        html.P(df['Not Confirmed'].sum()),
    ]),

    # Ventication orders
    html.Div([
        html.H3('Ventication'),
        html.P(df['Ventication'].sum()),
    ]),

    # NACH Pen orders
    html.Div([
        html.H3('NACH Pen'),
        html.P(df['NACH Pen'].sum()),
    ]),

    # Total revenue
    html.Div([
        html.H3('Total Revenue'),
        html.P(df['Revenue'].sum()),
    ]),

    # Current revenue
    html.Div([
        html.H3('Current Revenue'),
        html.P(df['Current Revenue'].sum()),
    ]),

    # Table of orders
    dcc.Table(
        id='orders-table',
        columns=[
            {'name': 'Order Id', 'id': 'order_id'},
            {'name': 'Order Punched Date', 'id': 'order_punched_date'},
            {'name': 'Incentive Date', 'id': 'incentive_date'},
            {'name': 'Order Status', 'id': 'order_status'},
            {'name': 'Punched Revenue', 'id': 'punched_revenue'},
            {'name': 'Current Revenue', 'id': 'current_revenue'},
            {'name': 'Product Revenue', 'id': 'product_revenue'},
        ],
        data=df.to_dict('records'),
    ),
])

# Run the application
if __name__ == '__main__':
    app.run_server(debug=True)
