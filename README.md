Apresentação 01/04/2026 
Exercícios da aula 9

Questões 1 e 2.

Contextualização breve dos exercícios, utilizar os dados disponibiizados de classe, scores e bounding boxes, para criar uma função
que obtenha as bounding boxes, dado uma classe. O uso da função zip será util.

Exemplo de uso:

ghci> selectBoundingBoxesForClass 1 boundingBoxes classes
[(100.0,150.0,250.0,380.0)]

Nome e tipo da função:

selectBoundingBoxesForClass :: Int -> [(Float, Float, Float, Float)] -> [Int] -> [(Float, Float, Float, Float)]
