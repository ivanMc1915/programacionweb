# EXAMEN Unidad I: Programacion Web
# <h3> DESARROLLADO POR:<br>Ivan Maldonado Carrizosa <br> PROFESOR: <br> Jose Arturo Bustamante Lazcano <br>Materia: <br>Programacion web</h3>
# <h5>Descripcion: <br>Muestra los Titanes del anime Shingeki no Kyoji, Su altura, y el origen de donde vienen tal cual los titanes</h5>
# CODIGO REALIZADO
```PYTHON && CSS
import streamlit as st
import requests
import base64


def set_background(image_file):
    with open(image_file, "rb") as f:
        encoded_string = base64.b64encode(f.read()).decode()
    
    st.markdown(
        f"""
        <style>
        .stApp {{
            background-image: url("data:image/png;base64,{encoded_string}");
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            background-attachment: fixed;
        }}
        </style>
        """,unsafe_allow_html=True
    )
set_background("img/shing.jpg")

st.set_page_config(page_title="SHINGEKI NO KYOJIN", layout="wide")

# Estilos
st.markdown("""
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Pirata+One&display=swap" rel="stylesheet');

        .shingeki-title {
            font-family: 'Pirata One', cursive;
                  font-size: 80px;
                  font-weight: bold;
                  text-align:center;
                  text-transform: uppercase;
                  letter-spacing: 5px;
                  margin:20px 0;

        background: linear-gradient(
            180deg, 
            #FFFFFF 00%, 
            #D8D8D8 30%, 
            #900C3F 45%, 
            #6E6E6E 60%, 
            #1A1A1A 100%
        );
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;

        filter: 
            drop-shadow(2px 2px 0px #000) 
            drop-shadow(-2px -2px 0px #000)
            drop-shadow(2px -2px 0px #000)
            drop-shadow(-2px 2px 0px #000)
            drop-shadow(0px 0px 12px rgba(0, 0, 0, 0.95))
            drop-shadow(0px 0px 25px rgba(0, 0, 0, 0.8));
            
        }
       
        .tarjeta-titan{
            background-color: #000;
                border: 4px solid #000;
                border-radius: 12px;
                padding: 10px;
                box-shadow: 4px 4px 0px #000;
                text-align: center;
                transition: transform 0.15s ease-in-out;
                }
        }

        .tarjeta-titan:hover {
            transform: translateY(-4px);
        }

        .tarjeta-titan-name {

        
               color: #FFFFFF;
               font-size: 14px;
               font-weight: bold;
               margin: 4px 0 0 0;
        }

        .titanes-badge {
            background-color: #70D1FE;
            color: #000;
            border: 2px solid #000;
            border-radius: 10px;
            display: inline-block;
            padding: 2px 10px;
            font-size: 13px;
            font-weight: bold;
            margin-bottom: 6px;
        }

        .titanes-occ {
            color: #FFFFFF;
            font-size: 14px;
            font-weight: bold;
            margin: 4px 0 0 0;
        }

        .titanes-img-box {
            background-color: #FFF;
            border: 3px solid #000;
            border-radius: 12px;
            padding: 8px;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 200px;
        }

        .titanes-img-box img {
            max-height: 100%;
            max-width: 100%;
            object-fit: contain;
        }
    </style>
""", unsafe_allow_html=True)

st.markdown('<div class="shingeki-title">SHINGEKI NO KYOJIN</div>', unsafe_allow_html=True)

response = requests.get("https://api.attackontitanapi.com/titans")
data = response.json()
titanes = data.get("results", [])

columnas = st.columns(4)

for i, t in enumerate(titanes):
    col = columnas[i % 4]
    

    raw_img = t.get("img", "")

    if ".png" in raw_img:
        img_url = raw_img.split(".png")[0] + ".png"
    elif ".jpg" in raw_img:
        img_url = raw_img.split(".jpg")[0] + ".jpg"
    else:
        img_url = raw_img



    nombre = t.get("name", "Desconocido")
    tamaño = t.get("height", "Sin registro")
    allegiance = t.get("allegiance", "Sin registro")


    with col:
        st.markdown(
            f"""
            <div class="tarjeta-titan">
                <img src="{img_url}" width="100%">
                <h3 class="tarjeta-titan-name">Nombre: {nombre}</h3>
                <p class="titanes-occ">Tamaño: {tamaño}<br></p>
                <p class="titanes-occ">Origen: {allegiance}</p>
            </div>
            """,
            unsafe_allow_html=True,
        )
   
```
# Muestra de la interfaz
![shingeki](/shingeki.png)
# Ejemplo de API:
Consultada en <https://api.attackontitanapi.com/titans>, y visulizada desde el inspector del navegador
![Api](/apiweb.png)
![API](/apinsp.png)
