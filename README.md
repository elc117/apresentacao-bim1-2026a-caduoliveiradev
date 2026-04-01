# Apresentação 01/04/2026 
## Exercícios da aula 9

- Questões 1 e 2.

  Contextualização breve dos exercícios, utilizar os dados disponibiizados de classe, scores e bounding boxes, para criar uma função
que obtenha as bounding boxes, dado uma classe. O uso da função zip será util.

- Exemplo de uso:
```hs
ghci> selectBoundingBoxesForClass 1 boundingBoxes classes
[(100.0,150.0,250.0,380.0)]
```
- Nome e tipo da função:
```hs
selectBoundingBoxesForClass :: Int -> [(Float, Float, Float, Float)] -> [Int] -> [(Float, Float, Float, Float)]
```
- Dados das listas:


<img width="716" height="302" alt="image" src="https://github.com/user-attachments/assets/dcdf4d43-7fe2-457d-aa90-11d9b26cec34" />

  O principio para resolver a questão é saber que as listas são **inter-relacionadas**, como por exemplo o primeiro objeto, de classe 0 score 0,95 e com bounding box (34.0, 60.0, 200.0, 320.0).


<img width="716" height="302" alt="Primeiro elemento com primeiro elemento com primeiro elemento" src="https://github.com/user-attachments/assets/83c23f22-5300-4ec1-aed6-eb8a540c96f4" />
