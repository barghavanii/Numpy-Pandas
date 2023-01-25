# Numpy-Pandas
Using Numpy &amp; pandas library 
import numpy as np
import pandas as pd
dfSeattle2014 = pd.read_csv('/content/Seattle2014-1.csv')
print(list(dfSeattle2014.columns))
print(dfSeattle2014)
print(dfSeattle2014.index)
from pandas.core.arrays.sparse import dtype
dfCaCities=pd.read_csv('/content/california_cities.csv')
print('Type of the "city" columns: ',dfCaCities['city'].dtypes)
print('Type of a single element of the "city" columns: ',type(dfCaCities['city'][0]))
print('Type of a single element of the "latd" columns: ',type(dfCaCities['latd'][0]))
print('dfCaCities number of dimensions: ',dfCaCities.ndim , '\ndfCaCities actual dimensions: ',dfCaCities.shape , '\ndfCaCities total number of elements found in dataframe: ',dfCaCities.size)
dfCaCities.info()
print(len(dfCaCities[dfCaCities['elevation_ft']>1000]))
print("total number of cities contained in the data: ", dfCaCities.city.notnull().sum())
print("total number of cities which contain more than one NaN value for that city: ", dfCaCities.isnull().any(axis=1).sum()) 
print("total number of cities which contain zero NaN in the data: ",dfCaCities.notnull().all(axis=1).sum())
print("cities which have more than one NaN value in the data for that city:\n", dfCaCities[dfCaCities.isnull().sum(axis=1)>1].city)
dfSeattle2014=pd.read_csv('/content/Seattle2014-1.csv')
dfSeattle2014['TMIN_C']=dfSeattle2014['TMIN']/10
dfSeattle2014['TMIN_F']=dfSeattle2014['TMIN_C']*9.0/5.0+32.0
dfSeattle2014[['TMIN','TMIN_C','TMIN_F']].head(10)
dfSeattle2014['PRCP_MM']=dfSeattle2014['PRCP']/10
dfSeattle2014['PRCP_IN']=dfSeattle2014['PRCP_MM']/25.4
dfSeattle2014['SNOW_MM']=dfSeattle2014['SNOW']/10
dfSeattle2014['SNOW_IN']=dfSeattle2014['SNOW_MM']/25.4
dfSeattle2014[['PRCP','PRCP_MM','PRCP_IN','SNOW','SNOW_MM','SNOW_IN']].head(10)
columns=['name','abbreviation','population','area','density']
dfStates=pd.read_csv('/content/state-abbrevs.csv').copy()
dfStateAreas=pd.read_csv('/content/state-areas.csv')
dfStatePop=pd.read_csv('/content/state-population.csv')
dfStates['area']=dfStateAreas['area (sq. mi)']
#print(dfStates,'\n count =',dfStates.iloc[:,0].count())
dfStates.set_index('abbreviation',inplace=True)
#print(dfStates,'\n count =',dfStates.iloc[:,0].count())
dfStatePop2012=dfStatePop[(dfStatePop.ages=='total')&(dfStatePop.year==2012)]
#print(dfStatePop2012,'\n count =',dfStatePop2012.iloc[:,0].count())
dfStatePop2012.set_index('state/region',inplace=True)

dfStates['pop']=(dfStatePop2012['population']).apply(int)
#print(dfStates,'\nn count = ',dfStates.iloc[:,0].count())
dfStates['density']=(dfStates['pop']/dfStates['area']).apply(int)
#print(dfStates,'\nn count = ',dfStates.iloc[:,0].count())

#8a
dfStates[dfStates['pop']>10000000]
dfStates[dfStates['density']>500]
data1={'col1':[1,2,3,4,5,np.nan,6,7,np.nan,8], 'col2':[11,12,np.nan,13,14,np.nan,15,16,np.nan,np.nan]}
df=pd.DataFrame(data1)
df
from pandas.core.common import any_none
any_nan=df.isnull().any(axis=1)
print('\nAny NaN:\n',any_nan)
not_any_nan=df.notnull().all(axis=1)
print('\nNo NaNs:\n',not_any_nan)
nan_counts=df.isnull().sum(axis=1)
print('\nNan counts:\n',nan_counts)
notnan_counts=df.notnull().sum(axis=1)
print('\nNot-Nan counts:\n',notnan_counts)
