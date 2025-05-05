import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv('C:/Users/Edmilson/Downloads/ecommerce_preparados.csv')
pd.set_option('display.width', None)
print(df.info())
print ('Valores nulos:\n', df.isnull().sum())

# Somente pontos de destaque:
novo_df= df.drop(labels= ['Desconto', 'Material', 'Temporada', 'Review1', 'Review2', 'Review3', 'Desconto_MinMax', 'Marca_Cod', 'Material_Cod', 'Temporada_Cod', 'Material_Freq'], axis=1, inplace=False)
print (novo_df.info())
print ('Valores nulos:\n', novo_df.isnull().sum())
novo_df.fillna(0, inplace= True)
novo_df.replace('', 0, inplace=True)

# Verificando a visualização de gênero a partir de porcentagem
print(novo_df['Gênero'].unique())
genero_freq = novo_df['Gênero'].value_counts()/len(novo_df)*100
novo_df['genero_freq'] = novo_df['Gênero'].map(genero_freq)
print(genero_freq)
percent = genero_freq.sum() # Certificação de que totalizaria 100%
print (percent)

# Tomada de decisão: excluir linhas de gêner que apresentam menos de 5% de ocorrência.
novo_df = novo_df[~novo_df['Gênero'].isin(['Sem gênero infantil', 'Mulher', 'roupa para gordinha pluss P ao 52', 'menino', 'bermuda feminina brilho Blogueira','short menina verao look mulher', 'Unissex'])]

print(novo_df.head())
print(novo_df.tail())
print(novo_df['Gênero'].unique())

#Modificações para melhor visualização
novo_df['Gênero'] = novo_df['Gênero'].str.strip().str.upper()
novo_df ['Marca'] = novo_df['Marca'].str.title()

#Salvando novo df para arquivo csv
novo_df.to_csv('Ecommerce_analise.csv', index=False)

# --------------------------------GRÁFICOS---------------------------------------
plt.figure(figsize=(15,20))

# Gênero
plt.subplot(4,3,1)
novo_df['Gênero'].value_counts().plot(kind='bar',color='purple')
plt.title('Produtos por gênero', fontsize=10)
plt.xlabel('Gênero', fontsize=6)
plt.xticks(rotation=0, fontsize=6)
plt.ylabel('Frequência', fontsize=6)
novo_df['gen_int'] = novo_df['Gênero'].astype('category').cat.codes +1

#Box plot
plt.subplot(4, 3, 2)
sns.boxplot(x='Gênero', y='Qtd_Vendidos_Cod', data=novo_df, palette='Set2')
plt.title('Distribuição de Vendas por Gênero', fontsize=10)
plt.xlabel('Gênero', fontsize=8)
plt.ylabel('Qtd Vendidos', fontsize=8)
plt.xticks(rotation=30, ha='right', fontsize=6)
plt.yticks(fontsize=6)
plt.yscale('log')


# Freq marcas
plt.subplot(4,3,3)
x = novo_df['Marca'].value_counts().head(10)
plt.pie(x.values, labels=x.index, autopct='%.1f%%', startangle=90, textprops={'fontsize':6})
plt.title('TOP 10 Marcas', fontsize=10)
print(novo_df['Marca'].value_counts().head(10))

# Mapa de calor
plt.subplot(4,3,7)
corr= novo_df[['Qtd_Vendidos_Cod', 'Preço', 'gen_int', 'N_Avaliações','Marca_Freq']].corr()
sns.heatmap(corr,annot=True,cmap='coolwarm',annot_kws={'size': 6})
plt.title('Correlação', fontsize=10)
plt.xticks(rotation=45, ha='right', fontsize=6)

# Gráfico de regressão
plt.subplot(4,3,5)
sns.regplot(x='Nota', y='N_Avaliações', data=novo_df, color='#d0bbff', scatter_kws={'alpha': 0.5, 'color': '#ff9f9b'})
plt.title('Regressão Avaliações e notas', fontsize=10)
plt.xlabel('Notas', fontsize=6)
plt.ylabel('N Avaliações', fontsize=6)

# Densidade
plt.subplot(4,3,6)
sns.kdeplot(novo_df['Preço'], fill=True, color='Purple')
plt.title('Moda de Preços', fontsize=10)
plt.xlabel('Preço')

# Histograma
plt.subplot(4,3,4)
plt.hist(novo_df['Nota'], bins=100, color='purple', alpha=0.8)
plt.title('Frequência de notas', fontsize= 10)
plt.xlabel('Nota')
plt.ylabel('Frequência')
plt.grid(True)

#Dispersão
plt.subplot(4, 3, 8)
sns.scatterplot(x='Marca_Freq', y='Preço', data=novo_df, alpha=0.6, color='#4caf50')
plt.title('Preço vs. Frequência da Marca', fontsize=10)
plt.xlabel('Frequência da Marca', fontsize=8)
plt.ylabel('Preço', fontsize=8)
plt.xticks(fontsize=6)
plt.yticks(fontsize=6)
plt.grid(True, linestyle='--', alpha=0.6)


plt.tight_layout()
plt.show()
