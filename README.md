# AdvancedGospiderMiner
#### Onde tiver twitch.tv, susbtitua pelo seu

## Começando spiders usando uma lista de urls vivas (listaUrlsParaSpider)
```
gospider -S listaUrlsParaSpider -d 4 -a | sort -u  > spider
```
```
cat spider | grep js | cut -d "[" -f3 | cut -d "]" -f1 | cut -d " " -f2 | grep twitch.tv >> spiderUniqueJs1column
```
```
cat spider | grep js | rev | cut -d " " -f1 | rev | grep twitch.tv  >> spiderUniqueJslastcolumn
```
```
cat spiderUnique* | sort -u > spiderAllSorted
```
```
xargs -P20 -a spiderAllSorted -I 'FUZZ' sh -c 'echo "\nURLALVO\n" >> allContentsFuzzSpider;curl -L -sf FUZZ 2>/dev/null >> allContentsFuzzSpider'
```

## Para buscar dentro dos resultados obtidos

### Você deve criar um arquivo chamado filterWordsMatch, onde vão ter as palavras que você quer buscar dentro dos JS do arquivo que vai conter todos os conteudos dos JS:
eg.:

graphql

localhost

### Utilize palavras que não dêem falso positivo nos JS
```
xargs -P10 -a filterWordsMatch -I 'FUZZ' sh -c 'egrep -o ".{1,20}FUZZ.{1,20}" allContentsFuzzSpider | grep -i --color FUZZ'
```
