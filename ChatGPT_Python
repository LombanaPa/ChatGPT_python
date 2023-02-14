import openai
import pandas as pd
import numpy as np
from tqdm import tqdm

openai.api_key = 'YOUR-API-KEY'

denominacion = pd.read_csv("Denominacion.csv", sep=";", encoding='latin1')

df_original = pd.DataFrame(columns=['Descripcion','ocupacion_cod','denominacion_cod','nombre_denominacion'])
for i in tqdm(denominacion.index):
    ocupacion_cod = denominacion.iat[i,1]
    denominacion_cod = denominacion.iat[i,3]
    nombre_denominacion = denominacion.iat[i,4]
    
    try:
        #text-embedding-ada-002 / text-davinci-003
        completion = openai.Completion.create(engine = "text-embedding-ada-002", prompt=f"¿Qué hace un {nombre_denominacion}?",
        n=1, max_tokens=300)

        completion_text = completion.choices[0].text
        df_paso = pd.DataFrame(np.array([completion_text.replace("\n", "")]),columns=['Descripcion'])
        df_paso['ocupacion_cod']=ocupacion_cod
        df_paso['denominacion_cod']=denominacion_cod
        df_paso['nombre_denominacion']=nombre_denominacion
        df_original = pd.concat([df_original,df_paso])
    except:
        print("Como que se nos jodio la token ome Pablo")
    if i==10:
        break
