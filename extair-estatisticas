import csv
from selenium import webdriver
import pandas as pd
driver = webdriver.Chrome()

orientador = []
autor = []
titulo = []
tipo = []
programa = []
data = []
downloads = []
paises = []
cidades = []
sempdf = []

url = 'https://bdtd.inpa.gov.br/xmlui/handle/tede/'

with open('tese_18-19.csv', newline='', encoding='utf-8') as a:
    teses = csv.reader(a)
    for i in teses:
        print('extraindo dados do elemento n.',i[0])
        handle = i[7]
        driver.get(url+handle+'/statistics')
        x = driver.find_elements_by_id('aspect_statistics_StatisticsTransformer_table_list-table')
        if len(x) == 5:
            try:
                download = x[2].find_element_by_id('aspect_statistics_StatisticsTransformer_cell_02').text
            except:
                download = 0
            downloads.append(download)
            pais = x[3].text.replace('Visualizações\n','').split('\n')
            paises.append(pais)
            cidade = x[4].text.replace('Visualizações\n','').split('\n')
            cidades.append(cidade)
        
            orientador.append(i[1])
            autor.append(i[2])
            titulo.append(i[3])
            tipo.append(i[4])
            programa.append(i[5])
            data.append(i[6])
        else:
            print('item sem pdf')
            sempdf.append(handle)
            
            
        
d = {'orientador':orientador,
     'autor':autor,
     'titulo': titulo,
     'tipo': tipo,
     'programa': programa,
     'data': data,
     'downloads': downloads,
     'paises': paises,
     'cidades':cidades}

df = pd.DataFrame(data=d)
df.to_csv('teses_estatisticas.csv')
