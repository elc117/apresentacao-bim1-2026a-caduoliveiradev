# Apresentação 01/04/2026 
## Exercícios da aula 9

- Questão 1.

  Contextualização breve dos exercícios, utilizar os dados disponibiizados de classe, scores e bounding boxes, para criar uma função
que obtenha as bounding boxes, dado uma classe. O uso da função zip será util.

- Exemplo de uso da função no terminal:
```hs
ghci> selectBoundingBoxesForClass 1 boundingBoxes classes
O que deve imprimir:
[(100.0,150.0,250.0,380.0)] (Dados da lista mostrada a seguir em imagem)
```
- Nome e tipo da função:
```hs
selectBoundingBoxesForClass :: Int -> [(Float, Float, Float, Float)] -> [Int] -> [(Float, Float, Float, Float)]
```
- Dados das listas:


<img width="716" height="302" alt="image" src="https://github.com/user-attachments/assets/dcdf4d43-7fe2-457d-aa90-11d9b26cec34" />

 - O principio para resolver a questão é saber que as listas são **inter-relacionadas**, como por exemplo o primeiro objeto, de classe 0 score 0,95 e com bounding box (34.0, 60.0, 200.0, 320.0).

<img width="716" height="302" alt="Primeiro elemento com primeiro elemento com primeiro elemento" src="https://github.com/user-attachments/assets/83c23f22-5300-4ec1-aed6-eb8a540c96f4" />

Mas o haskell não processa essa interação sozinho, portanto precisamos de algumas funções auxiliares para juntar as listas que coincidem e fazer a filtragem e limpar o que nao vamos precisar.

Para a função principal, eu comecei implementando a função de filtragem que será necessaria para comparar o número que buscamos com a classe encontrada, se for igual retornará true.
```hs
isCorrectClass :: Int -> ((Float, Float, Float, Float), Int) -> Bool
isCorrectClass targetClass (_, c) = c == targetClass
```
- Resumidamente, o número que nós procuramos (target) será comparado com uma tupla que virá da função principal que percorre as listas de bounding boxes e classes.
- **Dificuldade 1** - Não sabia como isolar apenas a parte da classe, pesquisando encontrei que utilizando um "_" ignoraria completamente aquela lista e seguiria a condicional apenas com o que sobrou.
- **Dificuldade 2** - Eu sabia o que tinha que fazer (comparações etc), mas tive um pouco de dificuldade para fazer essa sintaxe de receber o targetClass e fazer essa comparação porque visualmente é diferente do que estou acostumado com C.

- A segunda função auxiliar seria a que separaria a parte da classe da parte das bounding boxes. Para isso utilizei o mesmo principio de ignorar uma parte da tupla utilizando "_".
```hs
getBBox :: ((Float, Float, Float, Float), Int) -> (Float, Float, Float, Float)
getBBox (bbox, _) = bbox
```
- Aqui ele pega a tupla (ou tuplas) que resultou das comparações e testes e remove a classe, retornando apenas as bounding boxes.

## Com as Auxiliares prontas estava tudo pronto para a função principal.
- É nesse ponto que o **zip** se torna muito util, pois transformará essas listas recebidas em uma tupla para que elas possam ser usadas como parametro e alteradas.
- Exemplo visual:


<img width="343" height="149" alt="image" src="https://github.com/user-attachments/assets/4176afa3-addd-448f-a3c5-5a6474840eef" />


Dessa forma a função principal ficou desenvolvida assim:
```hs
selectBoundingBoxesForClass target bboxes cls = 
    map getBBox (filter (isCorrectClass target) (zip bboxes cls))
```
- A primeira coisa que acontece nessa função é o **zip** que junta as Bounding Boxes recebidas com as Classes formando tuplas.
- Depois disso o a função isCorrectClass vai comparar o targetClass com a Class das tuplas e com o uso do filter vai filtrar apenas as tuplas que tem a classe escolhida.
- Por ultimo, utilizei um map na função auxiliar que fiz getBBox que tira a parte das classes deixando apenas as Bounding Boxes correspondentes finalizando o exercicio.

Nessa função principal uma das **dificuldades** que tive para monta-la foi na parte de juntar o filter da auxiliar isCorrectClass com as listas. O zip resolveu isso pois transforma listas em uma tupla que é lida como uma lista só, que funciona no filter, por isso o zip precisa ser o primeiro a ser feito na função.

### Referências
https://github.com/AndreaInfUFSM/elc117-2026a

http://www.zvon.org/other/haskell/Outputprelude/zip_f.html
