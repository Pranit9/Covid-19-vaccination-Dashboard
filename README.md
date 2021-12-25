# Covid-19-vaccination-Dashboard
Dashboard code 
from __future__ import print_function
from ipywidgets import interact, interactive, fixed, interact_manual
from IPython.core.display import display, HTML

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import folium
import plotly.graph_objects as go
import seaborn as sns
import ipywidgets as widgets
import plotly.express as px
country_df = pd.read_csv('C:\\Users\\cw\\Desktop\\vaccination_excel.csv')
country_df.head(10)
country_df.columns = map(str.lower, country_df.columns)
country_df.columns
country_df.columns = map(str.lower, country_df.columns)
fig = go.FigureWidget( layout=go.Layout() )
def highlight_col(x):
    r = 'background-color: yellow'
    y = 'background-color: green'
   
    df1 = pd.DataFrame('', index=x.index, columns=x.columns)
    df1.iloc[:, 1] = y
    df1.iloc[:, 2] = r
   
    
    return df1

def show_people_vaccinated(n):
    n = int(n)
    return country_df.sort_values('doses given', ascending= False).head(n).style.apply(highlight_col, axis=None)

interact(show_people_vaccinated, n='10')

ipywLayout = widgets.Layout(border='solid 2px green')
ipywLayout.display='none'
widgets.VBox([fig], layout=ipywLayout)
sorted_country_df = country_df.sort_values('doses given', ascending=False).head(10)
fig = px.scatter(sorted_country_df.head(10), x='location', y='doses given', size='doses given',
                color='location', hover_name="doses given", size_max=80)

fig.show()
import plotly.graph_objects as go

def plot_people_vaccinated_in_world(country):
    labels = ['doses given', 'fully vaccinated']
    colors = ['blue', 'red']
    mode_size = [6,8]
    line_size = [4,5]
    
    df_list = [country_df]
    
    fig = go.Figure()
    
    for i, df in enumerate(df_list):
        if country == 'World' or country == 'World':
            x_data = np.array(list(df.iloc[:, 1:].columns))
                
        fig.add_trace(go.Scatter(x=x_data,  mode='lines+markers',
                                    name=labels[i],
                                    line = dict(color=colors[i], width=line_size[i]),
                                    connectgaps=True,
                                    text = "Total " + str(labels[i])
                                 
                                    ))
            
        fig.show()
            

interact(plot_people_vaccinated_in_world, country='World');
