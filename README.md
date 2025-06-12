# Análise Termodinâmica - ERA5 📈

> Neste repositório encontram-se códigos para gerar campos termodinâmicos e uma estimativa de sondagem com base nos dados da reanálise ERA5.

### Utilização dos scripts

Os scripts se encontram em .ipynb, que podem ser rodados pelo Google Colab ou pelo Jupyter Notebook. Caso queira rodar em alguma IDE (Spyder ou VSCODE), copie a parte dos códigos que estão completas em uma célula e cole na sua IDE de escolha. 


# 🗺️ Campos Termodinâmicos 

Aqui está um pequeno tutorial explicativo de como utilizar o script e o que ele faz.

## Bibliotecas necessárias

Para utilizar o script, algumas bibliotecas devem ser instaladas: 
```
!pip install metpy cartopy
```
> Existem células prontas para a instalação nos scripts.

## Utilizando o Script

O script começa importando o Google Drive e instalando as bibliotecas necessárias, caso queira usa-lo no Google Colab 
```
from google.colab import drive
drive.mount('/content/drive')
```

A primeira parte do script, insira o seu próprio diretório:
```
ds = xr.open_dataset('/content/drive/MyDrive/Meteoro_UFRJ/ES2 Aanlise/termo.nc')
```
Após isso, edite o recorte da região de estudo e a série temporal:

```
lon_slice = slice(-45., -40.)
lat_slice = slice(-20., -24.)
ds = ds.sel(latitude=lat_slice, longitude=lon_slice, valid_time='2024-12-16T12:00:00')
```

Caso queria adicionar mais índices, adicione a variável nos arrays e depois no loop de cálculos.

## Campos

Para mudar a região que será plotada no campo, edite essa parte: 
```
ax.set_extent([-45, -40.75, -24, -20.5], crs=ccrs.PlateCarree())
```
Para mudar o shapefile, insira o diretorio do seu shapefile. Caso queira mudar o intervalo, colormap e método de extensão da colorbar:
```
shapefile = list(shpreader.Reader('/content/drive/MyDrive/Meteoro_UFRJ/Estágio Supervisionado 2 (Briefing)/Scripts/shapefiles/BR_UF_2021/BR_UF_2021.shp').geometries())
```
```
cape = ax.contourf(ds.longitude,
                ds.latitude,
                cape_arr,
                cmap='GnBu', # Colormap
                extend = 'max', # Extensão
                levels=np.arange(0, 2000, 200)) # Intervalos
```

## Exemplo de campo termodinâmico

<img src="https://github.com/user-attachments/assets/8addd190-fc08-48d1-a91b-f7bd9ed8c6d3" width="600">





# 📈 Estimativa de Sondagem - ERA5

Aqui está um pequeno tutorial ou guia de como usar o script e o que ele faz.

## Bibliotecas Necessárias

Para rodar o script da estimativativa de sondagem, primeiro precisamos instalar o metpy:
```
!pip install metpy
```
> Existem células prontas para a instalação nos scripts.

## Utilizando o Script

O script começa importando o Google Drive e instalando as bibliotecas necessárias, caso queira usa-lo no Google Colab 
```
from google.colab import drive
drive.mount('/content/drive')
```

A primeira parte do script, insira o seu próprio diretório:
```
ds = xr.open_dataset('/content/drive/MyDrive/Meteoro_UFRJ/ES2 Aanlise/sounding.nc')
```
Após isso, edite o recorte da região de estudo e a data:

```
lat = -22.48
lon = -43.15
time = '2024-12-16T18:00'
```
Basicamente, não há nada mais para mexer no código, apenas rodar e plotar o skew-t. Apenas mude, caso queira, o tamanho da figura ou adicione mais indices para serem calculados.

## Exemplo de Sondagem
<img src="https://github.com/user-attachments/assets/120964bf-cddb-4d8b-9ad2-8a291f4fb1af" width="500">

## Contribuidores

<a href="https://github.com/GHMachado/Plots_Satelite_GOES16/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=GHMachado/Plots_Satelite_GOES16" />
</a>

